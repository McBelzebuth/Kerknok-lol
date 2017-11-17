// ==UserScript==
// @name         Script pour lol
// @namespace    http://tampermonkey.net/
// @version      0.1
// @include     http://landsoflords.com/*
// @include     http://www.landsoflords.com/*
// @include     https://landsoflords.com/*
// @include     https://www.landsoflords.com/*
// @description  try to take over the world!
// @author       McBelzebuth
// @grant       GM_xmlhttpRequest
// @grant       GM_getValue
// @grant       GM_setValue
// @grant       GM_addStyle
// ==/UserScript==

(function() {
    var script = {
        domain: '',
        gold: '0',
        user: '',
        hab: '0',
        happyness: '0',
        start: function() {
            this.checkPage();
        },
        checkPage : function() {
            this.log("CheckPage");
            var tmp;
            var user;
            var time;
            if (window.location.pathname.indexOf("/mgmt/") > -1 && window.location.pathname.indexOf("/res:") > -1) {
                tmp = window.location.pathname.substr(window.location.pathname.indexOf('/mgmt/')+6);
                this.domain = tmp.substr(0,tmp.indexOf('/'));
                user = document.getElementById('user');
                this.user = user.getAttribute('title');
                time = Date.now();
                var keyM = this.domain+'money';
                if (GM_getValue(keyM) && time < GM_getValue(keyM)+3600000)
                {
                    this.log('money already exported this hour');
                    this.log('now:'+time);
                    this.log('old:'+GM_getValue(keyM));
                }
                else
                {
                    this.log('money not exported this hour');
                    GM_setValue(keyM, time);
                    this.getMoney();
                }
            }
            else if (window.location.pathname.indexOf("/mgmt/") > -1 && window.location.pathname.indexOf("/units") > -1) {
                tmp = window.location.pathname.substr(window.location.pathname.indexOf('/mgmt/')+6);
                this.domain = tmp.substr(0,tmp.indexOf('/'));
                user = document.getElementById('user');
                this.user = user.getAttribute('title');
                time = Date.now();
                var keyH = this.domain+'hab';
                if (GM_getValue(keyH) && time < GM_getValue(keyH)+3600000)
                {
                    this.log('hab already exported this hour');
                    this.log('now:'+time);
                    this.log('old:'+GM_getValue(keyH));
                }
                else
                {
                    this.log('hab not exported this hour');
                    GM_setValue(keyH, time);
                    this.getHab();
                }
            }
        },

        getMoney: function() {
            var golds = document.getElementById('money');
            this.gold = golds.innerText.replace('.',',');
            this.postToGoogleMoney();
        },
        getHab: function() {
            var x = document.getElementsByClassName("mgmtinfo");
            var span = x[0].getElementsByTagName("span");
            this.hab = span[0].innerHTML;
            span = x[2].getElementsByTagName("span");
            var happyness = span[0].innerHTML;
            this.happyness = happyness.replace('%','');
            this.postToGoogleHab();
        },

        log: function(data) {
            if (debug) console.log(data);
        },

        postToGoogleMoney: function(data) {
            $.ajax({
                url: "https://docs.google.com/forms/d/1IJguUHkPGpCmjZhGNtdVz0uUEw1niVpWCxDoFXxzmLk/formResponse",
                data: {"entry.1767415143": this.user,
                       "entry.601102438": this.domain,
                       "entry.333979560": this.gold},
                type: "POST",
                dataType: "xml",
                statusCode: {
                    0: function() {
                        this.log("datas send to google form");
                    },
                    200: function() {
                        this.log("Error to send datas");
                    }
                }
            });
        },
        postToGoogleHab: function(data) {
            $.ajax({
                url: "https://docs.google.com/forms/d/1naLe7fXCmXerfQ1gQ0X4q5EYcjPxkzhIKUDw8nEfgGs/formResponse",
                data: {"entry.98694735": this.user,
                       "entry.1171633749": this.domain,
                       "entry.1681075849": this.hab,
                       "entry.745770450": this.happyness},
                type: "POST",
                dataType: "xml",
                statusCode: {
                    0: function() {
                        this.log("datas send to google form");
                    },
                    200: function() {
                        this.log("Error to send datas");
                    }
                }
            });
        }
    };
    script.start();
})();
