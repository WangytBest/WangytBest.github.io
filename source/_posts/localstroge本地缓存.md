---
title: localstroge本地缓存
date: 2018-05-30 15:01:25
categories: [Javascript, util]

tags:
---

localStorage设置过期时间
<!-- more -->
```js
define("localStorage", function(require, exports, module){
    var cache = require("cachev1").local;
    var Promise = require("promise.min");

    /**
     * 将过期时间字符串转换成时间戳
     *  convertExpire("7d")
     *  convertExpire(3600)  1小时
     * @param  {String} val  过期时间，格式为`\d+[smhd]`，其中s 表示秒、m 分钟、h 小时、d 天，如 30d   默认是秒
     * @return {Number}      时间戳（单位s）
     */
    function convertExpire(val) {
        if (!val) return 0;

        var matches = ('' + val).match(/(\d+)([smhd])/);
        var ms = 0;

        if (matches) {
            switch (matches[2]) {
                case 's':
                    ms = matches[1];
                    break;
                case 'm':
                    ms = matches[1] * 60;
                    break;
                case 'h':
                    ms = matches[1] * 60 * 60;
                    break;
                case 'd':
                    ms = matches[1] * 24 * 60 * 60;
            }
        } else{
            ms = val;
        }
        return ms;
    }
    var timeout = setTimeout;
    var storage = {
        /**
         * 将数据写入本地缓存
         *
         * @param  {String}          key      键名
         * @param  {Object | String} value    数据
         * @param  {Object}          options  可选项，可传expire 设定数据过期时间，格式参见convertExpire
         *
         * @return {Promise}         Promise实例
         */
        set:function(key, value, options) {
            return new Promise(function(resolve, reject){
                var expire = convertExpire(typeof options == 'object' && options.expire ? options.expire : '7d');
                timeout(function () {
                    cache.setItem(key,value,expire,function (ret) {
                        if(ret==0) resolve();
                        else reject();
                    });
                });
            })
        },

        /**
         * 获取本地缓存数据，当数据已过期时会被清理掉
         *
         * @param  {String}  key         键名
         * @param  {Mix}     defaultVal  如设置了默认值，则保证不会被reject
         *
         * @return {Promise}      Promise实例
         */
        get:function(key, defaultVal) {
            return new Promise(function(resolve, reject){
                timeout(function () {
                    var value = cache.getItem(key);
                    if(value===""||value===null){
                        if(typeof defaultVal!="undefined"){
                            resolve(defaultVal);
                        }else{
                            reject();
                        }
                        return;
                    }
                    resolve(value);
                });
            })
        },

        /**
         * 移除本地缓存数据
         */
        remove:function(key) {
            return new Promise(function(resolve, reject){
                timeout(function () {
                    cache.removeItem(key);
                    resolve();
                });
            })
        },

        /**
         * 同步地设置本地缓存数据
         *
         * @deprecated 此方法只为了暂时兼容旧接口，会极大的影响性，能请勿使用！
         */
        setSync:function(key, value, options) {
            var expire = convertExpire(typeof options == 'object' && options.expire ? options.expire : '7d')
            cache.setItem(key,value,expire);
        },

        /**
         * 同步地获取本地缓存数据，当数据已过期时会被清理掉
         *
         * @deprecated 此方法只为了暂时兼容旧接口，会极大的影响性，能请勿使用！
         */
        getSync:function(key) {
            return cache.getItem(key);
        }
    }


    module.exports = storage;
});

```