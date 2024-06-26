/*! @sentry/browser 7.38.0 (a6cae1a) | https://github.com/getsentry/sentry-javascript */
var Sentry = function(t) {
    var n = function(t, r) {
        return n = Object.setPrototypeOf || {
            __proto__: []
        }instanceof Array && function(t, n) {
            t.__proto__ = n
        }
        || function(t, n) {
            for (var r in n)
                Object.prototype.hasOwnProperty.call(n, r) && (t[r] = n[r])
        }
        ,
        n(t, r)
    };
    function r(t, r) {
        if ("function" != typeof r && null !== r)
            throw new TypeError("Class extends value " + String(r) + " is not a constructor or null");
        function e() {
            this.constructor = t
        }
        n(t, r),
        t.prototype = null === r ? Object.create(r) : (e.prototype = r.prototype,
        new e)
    }
    var e = function() {
        return e = Object.assign || function(t) {
            for (var n, r = 1, e = arguments.length; r < e; r++)
                for (var i in n = arguments[r])
                    Object.prototype.hasOwnProperty.call(n, i) && (t[i] = n[i]);
            return t
        }
        ,
        e.apply(this, arguments)
    };
    function i(t) {
        var n = "function" == typeof Symbol && Symbol.iterator
          , r = n && t[n]
          , e = 0;
        if (r)
            return r.call(t);
        if (t && "number" == typeof t.length)
            return {
                next: function() {
                    return t && e >= t.length && (t = void 0),
                    {
                        value: t && t[e++],
                        done: !t
                    }
                }
            };
        throw new TypeError(n ? "Object is not iterable." : "Symbol.iterator is not defined.")
    }
    function o(t, n) {
        var r = "function" == typeof Symbol && t[Symbol.iterator];
        if (!r)
            return t;
        var e, i, o = r.call(t), u = [];
        try {
            for (; (void 0 === n || n-- > 0) && !(e = o.next()).done; )
                u.push(e.value)
        } catch (t) {
            i = {
                error: t
            }
        } finally {
            try {
                e && !e.done && (r = o.return) && r.call(o)
            } finally {
                if (i)
                    throw i.error
            }
        }
        return u
    }
    function u() {
        for (var t = [], n = 0; n < arguments.length; n++)
            t = t.concat(o(arguments[n]));
        return t
    }
    var a = Object.prototype.toString;
    function f(t) {
        switch (a.call(t)) {
        case "[object Error]":
        case "[object Exception]":
        case "[object DOMException]":
            return !0;
        default:
            return m(t, Error)
        }
    }
    function c(t, n) {
        return a.call(t) === "[object " + n + "]"
    }
    function s(t) {
        return c(t, "ErrorEvent")
    }
    function v(t) {
        return c(t, "DOMError")
    }
    function h(t) {
        return c(t, "String")
    }
    function l(t) {
        return null === t || "object" != typeof t && "function" != typeof t
    }
    function d(t) {
        return c(t, "Object")
    }
    function y(t) {
        return "undefined" != typeof Event && m(t, Event)
    }
    function p(t) {
        return Boolean(t && t.then && "function" == typeof t.then)
    }
    function m(t, n) {
        try {
            return t instanceof n
        } catch (t) {
            return !1
        }
    }
    function b(t) {
        return t && t.Math == Math ? t : void 0
    }
    var g = "object" == typeof globalThis && b(globalThis) || "object" == typeof window && b(window) || "object" == typeof self && b(self) || "object" == typeof global && b(global) || function() {
        return this
    }() || {};
    function w() {
        return g
    }
    function E(t, n, r) {
        var e = r || g
          , i = e.__SENTRY__ = e.__SENTRY__ || {};
        return i[t] || (i[t] = n())
    }
    var _ = w();
    function j(t, n) {
        void 0 === n && (n = {});
        try {
            for (var r = t, e = [], i = 0, o = 0, u = " > ".length, a = void 0, f = Array.isArray(n) ? n : n.keyAttrs, c = !Array.isArray(n) && n.maxStringLength || 80; r && i++ < 5 && !("html" === (a = k(r, f)) || i > 1 && o + e.length * u + a.length >= c); )
                e.push(a),
                o += a.length,
                r = r.parentNode;
            return e.reverse().join(" > ")
        } catch (t) {
            return "<unknown>"
        }
    }
    function k(t, n) {
        var r, e, i, o, u, a = t, f = [];
        if (!a || !a.tagName)
            return "";
        f.push(a.tagName.toLowerCase());
        var c = n && n.length ? n.filter((function(t) {
            return a.getAttribute(t)
        }
        )).map((function(t) {
            return [t, a.getAttribute(t)]
        }
        )) : null;
        if (c && c.length)
            c.forEach((function(t) {
                f.push("[" + t[0] + '="' + t[1] + '"]')
            }
            ));
        else if (a.id && f.push("#" + a.id),
        (r = a.className) && h(r))
            for (e = r.split(/\s+/),
            u = 0; u < e.length; u++)
                f.push("." + e[u]);
        var s = ["aria-label", "type", "name", "title", "alt"];
        for (u = 0; u < s.length; u++)
            i = s[u],
            (o = a.getAttribute(i)) && f.push("[" + i + '="' + o + '"]');
        return f.join("")
    }
    var S = function(t) {
        function n(n, r) {
            var e = this.constructor;
            void 0 === r && (r = "warn");
            var i = t.call(this, n) || this;
            return i.message = n,
            i.name = e.prototype.constructor.name,
            Object.setPrototypeOf(i, e.prototype),
            i.logLevel = r,
            i
        }
        return r(n, t),
        n
    }(Error)
      , x = /^(?:(\w+):)\/\/(?:(\w+)(?::(\w+)?)?@)([\w.-]+)(?::(\d+))?\/(.+)/;
    function O(t, n) {
        void 0 === n && (n = !1);
        var r = t.host
          , e = t.path
          , i = t.pass
          , o = t.port
          , u = t.projectId;
        return t.protocol + "://" + t.publicKey + (n && i ? ":" + i : "") + "@" + r + (o ? ":" + o : "") + "/" + (e ? e + "/" : e) + u
    }
    function R(t) {
        return {
            protocol: t.protocol,
            publicKey: t.publicKey || "",
            pass: t.pass || "",
            host: t.host,
            port: t.port || "",
            path: t.path || "",
            projectId: t.projectId
        }
    }
    function T(t) {
        return "string" == typeof t ? function(t) {
            var n = x.exec(t);
            if (!n)
                throw new S("Invalid Sentry Dsn: " + t);
            var r = o(n.slice(1), 6)
              , e = r[0]
              , i = r[1]
              , u = r[2]
              , a = void 0 === u ? "" : u
              , f = r[3]
              , c = r[4]
              , s = void 0 === c ? "" : c
              , v = ""
              , h = r[5]
              , l = h.split("/");
            if (l.length > 1 && (v = l.slice(0, -1).join("/"),
            h = l.pop()),
            h) {
                var d = h.match(/^\d+/);
                d && (h = d[0])
            }
            return R({
                host: f,
                pass: a,
                path: v,
                projectId: h,
                port: s,
                protocol: e,
                publicKey: i
            })
        }(t) : R(t)
    }
    var D, N = ["debug", "info", "warn", "error", "log", "assert", "trace"];
    function A(t, n) {
        return void 0 === n && (n = 0),
        "string" != typeof t || 0 === n || t.length <= n ? t : t.slice(0, n) + "..."
    }
    function I(t, n) {
        if (!Array.isArray(t))
            return "";
        for (var r = [], e = 0; e < t.length; e++) {
            var i = t[e];
            try {
                r.push(String(i))
            } catch (t) {
                r.push("[value cannot be serialized]")
            }
        }
        return r.join(n)
    }
    function M(t, n, r) {
        return void 0 === r && (r = !1),
        !!h(t) && (c(n, "RegExp") ? n.test(t) : !!h(n) && (r ? t === n : t.includes(n)))
    }
    function L(t, n, r) {
        return void 0 === n && (n = []),
        void 0 === r && (r = !1),
        n.some((function(n) {
            return M(t, n, r)
        }
        ))
    }
    function C(t, n, r) {
        if (n in t) {
            var e = t[n]
              , i = r(e);
            if ("function" == typeof i)
                try {
                    U(i, e)
                } catch (t) {}
            t[n] = i
        }
    }
    function q(t, n, r) {
        Object.defineProperty(t, n, {
            value: r,
            writable: !0,
            configurable: !0
        })
    }
    function U(t, n) {
        var r = n.prototype || {};
        t.prototype = n.prototype = r,
        q(t, "__sentry_original__", n)
    }
    function H(t) {
        return t.__sentry_original__
    }
    function P(t) {
        if (f(t))
            return e({
                message: t.message,
                name: t.name,
                stack: t.stack
            }, $(t));
        if (y(t)) {
            var n = e({
                type: t.type,
                target: X(t.target),
                currentTarget: X(t.currentTarget)
            }, $(t));
            return "undefined" != typeof CustomEvent && m(t, CustomEvent) && (n.detail = t.detail),
            n
        }
        return t
    }
    function X(t) {
        try {
            return n = t,
            "undefined" != typeof Element && m(n, Element) ? j(t) : Object.prototype.toString.call(t)
        } catch (t) {
            return "<unknown>"
        }
        var n
    }
    function $(t) {
        if ("object" == typeof t && null !== t) {
            var n = {};
            for (var r in t)
                Object.prototype.hasOwnProperty.call(t, r) && (n[r] = t[r]);
            return n
        }
        return {}
    }
    function F(t, n) {
        void 0 === n && (n = 40);
        var r = Object.keys(P(t));
        if (r.sort(),
        !r.length)
            return "[object has no keys]";
        if (r[0].length >= n)
            return A(r[0], n);
        for (var e = r.length; e > 0; e--) {
            var i = r.slice(0, e).join(", ");
            if (!(i.length > n))
                return e === r.length ? i : A(i, n)
        }
        return ""
    }
    function W(t) {
        return B(t, new Map)
    }
    function B(t, n) {
        var r, e;
        if (d(t)) {
            if (void 0 !== (c = n.get(t)))
                return c;
            var o = {};
            n.set(t, o);
            try {
                for (var u = i(Object.keys(t)), a = u.next(); !a.done; a = u.next()) {
                    var f = a.value;
                    void 0 !== t[f] && (o[f] = B(t[f], n))
                }
            } catch (t) {
                r = {
                    error: t
                }
            } finally {
                try {
                    a && !a.done && (e = u.return) && e.call(u)
                } finally {
                    if (r)
                        throw r.error
                }
            }
            return o
        }
        if (Array.isArray(t)) {
            var c;
            if (void 0 !== (c = n.get(t)))
                return c;
            var s = [];
            return n.set(t, s),
            t.forEach((function(t) {
                s.push(B(t, n))
            }
            )),
            s
        }
        return t
    }
    D = {
        enable: function() {},
        disable: function() {}
    },
    N.forEach((function(t) {
        D[t] = function() {}
    }
    ));
    var J = new Map;
    function z() {
        for (var t = [], n = 0; n < arguments.length; n++)
            t[n] = arguments[n];
        var r = t.sort((function(t, n) {
            return t[0] - n[0]
        }
        )).map((function(t) {
            return t[1]
        }
        ));
        return function(t, n) {
            var e, o, u, a, f, c;
            void 0 === n && (n = 0);
            var s = []
              , v = function(t) {
                var n = J.get(t);
                n || (n = new Map,
                J.set(t, n));
                var r = g.t;
                r && Object.keys(r).forEach((function(e) {
                    e.split("\n").forEach((function(i) {
                        var o = t(i);
                        o && o.filename && n.set(o.filename, r[e])
                    }
                    ))
                }
                ))
            };
            try {
                for (var h = i(r), l = h.next(); !l.done; l = h.next()) {
                    v(E = l.value)
                }
            } catch (t) {
                e = {
                    error: t
                }
            } finally {
                try {
                    l && !l.done && (o = h.return) && o.call(h)
                } finally {
                    if (e)
                        throw e.error
                }
            }
            try {
                for (var d = i(t.split("\n").slice(n)), y = d.next(); !y.done; y = d.next()) {
                    var p = y.value;
                    if (!(p.length > 1024)) {
                        var m = p.replace(/\(error: (.*)\)/, "$1");
                        try {
                            for (var b = (f = void 0,
                            i(r)), w = b.next(); !w.done; w = b.next()) {
                                var E, _ = (E = w.value)(m);
                                if (_) {
                                    var j = J.get(E);
                                    if (j && _.filename) {
                                        var k = j.get(_.filename);
                                        k && (_.debug_id = k)
                                    }
                                    s.push(_);
                                    break
                                }
                            }
                        } catch (t) {
                            f = {
                                error: t
                            }
                        } finally {
                            try {
                                w && !w.done && (c = b.return) && c.call(b)
                            } finally {
                                if (f)
                                    throw f.error
                            }
                        }
                    }
                }
            } catch (t) {
                u = {
                    error: t
                }
            } finally {
                try {
                    y && !y.done && (a = d.return) && a.call(d)
                } finally {
                    if (u)
                        throw u.error
                }
            }
            return G(s)
        }
    }
    function G(t) {
        if (!t.length)
            return [];
        var n = t
          , r = n[0].function || ""
          , i = n[n.length - 1].function || "";
        return -1 === r.indexOf("captureMessage") && -1 === r.indexOf("captureException") || (n = n.slice(1)),
        -1 !== i.indexOf("sentryWrapped") && (n = n.slice(0, -1)),
        n.slice(0, 50).map((function(t) {
            return e(e({}, t), {
                filename: t.filename || n[0].filename,
                function: t.function || "?"
            })
        }
        )).reverse()
    }
    var K = "<anonymous>";
    function V(t) {
        try {
            return t && "function" == typeof t && t.name || K
        } catch (t) {
            return K
        }
    }
    var Y = w();
    function Q() {
        if (!("fetch"in Y))
            return !1;
        try {
            return new Headers,
            new Request("http://www.example.com"),
            new Response,
            !0
        } catch (t) {
            return !1
        }
    }
    function Z(t) {
        return t && /^function fetch\(\)\s+\{\s+\[native code\]\s+\}$/.test(t.toString())
    }
    var tt, nt = w(), rt = {}, et = {};
    function it(t) {
        if (!et[t])
            switch (et[t] = !0,
            t) {
            case "console":
                !function() {
                    if (!("console"in nt))
                        return;
                    N.forEach((function(t) {
                        t in nt.console && C(nt.console, t, (function(n) {
                            return function() {
                                for (var r = [], e = 0; e < arguments.length; e++)
                                    r[e] = arguments[e];
                                ut("console", {
                                    args: r,
                                    level: t
                                }),
                                n && n.apply(nt.console, r)
                            }
                        }
                        ))
                    }
                    ))
                }();
                break;
            case "dom":
                !function() {
                    if (!("document"in nt))
                        return;
                    var t = ut.bind(null, "dom")
                      , n = vt(t, !0);
                    nt.document.addEventListener("click", n, !1),
                    nt.document.addEventListener("keypress", n, !1),
                    ["EventTarget", "Node"].forEach((function(n) {
                        var r = nt[n] && nt[n].prototype;
                        r && r.hasOwnProperty && r.hasOwnProperty("addEventListener") && (C(r, "addEventListener", (function(n) {
                            return function(r, e, i) {
                                if ("click" === r || "keypress" == r)
                                    try {
                                        var o = this
                                          , u = o.__sentry_instrumentation_handlers__ = o.__sentry_instrumentation_handlers__ || {}
                                          , a = u[r] = u[r] || {
                                            refCount: 0
                                        };
                                        if (!a.handler) {
                                            var f = vt(t);
                                            a.handler = f,
                                            n.call(this, r, f, i)
                                        }
                                        a.refCount++
                                    } catch (t) {}
                                return n.call(this, r, e, i)
                            }
                        }
                        )),
                        C(r, "removeEventListener", (function(t) {
                            return function(n, r, e) {
                                if ("click" === n || "keypress" == n)
                                    try {
                                        var i = this
                                          , o = i.__sentry_instrumentation_handlers__ || {}
                                          , u = o[n];
                                        u && (u.refCount--,
                                        u.refCount <= 0 && (t.call(this, n, u.handler, e),
                                        u.handler = void 0,
                                        delete o[n]),
                                        0 === Object.keys(o).length && delete i.__sentry_instrumentation_handlers__)
                                    } catch (t) {}
                                return t.call(this, n, r, e)
                            }
                        }
                        )))
                    }
                    ))
                }();
                break;
            case "xhr":
                !function() {
                    if (!("XMLHttpRequest"in nt))
                        return;
                    var t = XMLHttpRequest.prototype;
                    C(t, "open", (function(t) {
                        return function() {
                            for (var n = [], r = 0; r < arguments.length; r++)
                                n[r] = arguments[r];
                            var e = this
                              , i = n[1]
                              , o = e.__sentry_xhr__ = {
                                method: h(n[0]) ? n[0].toUpperCase() : n[0],
                                url: n[1]
                            };
                            h(i) && "POST" === o.method && i.match(/sentry_key/) && (e.__sentry_own_request__ = !0);
                            var u = function() {
                                if (4 === e.readyState) {
                                    try {
                                        o.status_code = e.status
                                    } catch (t) {}
                                    ut("xhr", {
                                        args: n,
                                        endTimestamp: Date.now(),
                                        startTimestamp: Date.now(),
                                        xhr: e
                                    })
                                }
                            };
                            return "onreadystatechange"in e && "function" == typeof e.onreadystatechange ? C(e, "onreadystatechange", (function(t) {
                                return function() {
                                    for (var n = [], r = 0; r < arguments.length; r++)
                                        n[r] = arguments[r];
                                    return u(),
                                    t.apply(e, n)
                                }
                            }
                            )) : e.addEventListener("readystatechange", u),
                            t.apply(e, n)
                        }
                    }
                    )),
                    C(t, "send", (function(t) {
                        return function() {
                            for (var n = [], r = 0; r < arguments.length; r++)
                                n[r] = arguments[r];
                            return this.__sentry_xhr__ && void 0 !== n[0] && (this.__sentry_xhr__.body = n[0]),
                            ut("xhr", {
                                args: n,
                                startTimestamp: Date.now(),
                                xhr: this
                            }),
                            t.apply(this, n)
                        }
                    }
                    ))
                }();
                break;
            case "fetch":
                !function() {
                    if (!function() {
                        if (!Q())
                            return !1;
                        if (Z(Y.fetch))
                            return !0;
                        var t = !1
                          , n = Y.document;
                        if (n && "function" == typeof n.createElement)
                            try {
                                var r = n.createElement("iframe");
                                r.hidden = !0,
                                n.head.appendChild(r),
                                r.contentWindow && r.contentWindow.fetch && (t = Z(r.contentWindow.fetch)),
                                n.head.removeChild(r)
                            } catch (t) {}
                        return t
                    }())
                        return;
                    C(nt, "fetch", (function(t) {
                        return function() {
                            for (var n = [], r = 0; r < arguments.length; r++)
                                n[r] = arguments[r];
                            var i = {
                                args: n,
                                fetchData: {
                                    method: at(n),
                                    url: ft(n)
                                },
                                startTimestamp: Date.now()
                            };
                            return ut("fetch", e({}, i)),
                            t.apply(nt, n).then((function(t) {
                                return ut("fetch", e(e({}, i), {
                                    endTimestamp: Date.now(),
                                    response: t
                                })),
                                t
                            }
                            ), (function(t) {
                                throw ut("fetch", e(e({}, i), {
                                    endTimestamp: Date.now(),
                                    error: t
                                })),
                                t
                            }
                            ))
                        }
                    }
                    ))
                }();
                break;
            case "history":
                !function() {
                    if (!function() {
                        var t = Y.chrome
                          , n = t && t.app && t.app.runtime
                          , r = "history"in Y && !!Y.history.pushState && !!Y.history.replaceState;
                        return !n && r
                    }())
                        return;
                    var t = nt.onpopstate;
                    function n(t) {
                        return function() {
                            for (var n = [], r = 0; r < arguments.length; r++)
                                n[r] = arguments[r];
                            var e = n.length > 2 ? n[2] : void 0;
                            if (e) {
                                var i = tt
                                  , o = String(e);
                                tt = o,
                                ut("history", {
                                    from: i,
                                    to: o
                                })
                            }
                            return t.apply(this, n)
                        }
                    }
                    nt.onpopstate = function() {
                        for (var n = [], r = 0; r < arguments.length; r++)
                            n[r] = arguments[r];
                        var e = nt.location.href
                          , i = tt;
                        if (tt = e,
                        ut("history", {
                            from: i,
                            to: e
                        }),
                        t)
                            try {
                                return t.apply(this, n)
                            } catch (t) {}
                    }
                    ,
                    C(nt.history, "pushState", n),
                    C(nt.history, "replaceState", n)
                }();
                break;
            case "error":
                ht = nt.onerror,
                nt.onerror = function(t, n, r, e, i) {
                    return ut("error", {
                        column: e,
                        error: i,
                        line: r,
                        msg: t,
                        url: n
                    }),
                    !!ht && ht.apply(this, arguments)
                }
                ;
                break;
            case "unhandledrejection":
                dt = nt.onunhandledrejection,
                nt.onunhandledrejection = function(t) {
                    return ut("unhandledrejection", t),
                    !dt || dt.apply(this, arguments)
                }
                ;
                break;
            default:
                return
            }
    }
    function ot(t, n) {
        rt[t] = rt[t] || [],
        rt[t].push(n),
        it(t)
    }
    function ut(t, n) {
        var r, e;
        if (t && rt[t])
            try {
                for (var o = i(rt[t] || []), u = o.next(); !u.done; u = o.next()) {
                    var a = u.value;
                    try {
                        a(n)
                    } catch (t) {}
                }
            } catch (t) {
                r = {
                    error: t
                }
            } finally {
                try {
                    u && !u.done && (e = o.return) && e.call(o)
                } finally {
                    if (r)
                        throw r.error
                }
            }
    }
    function at(t) {
        return void 0 === t && (t = []),
        "Request"in nt && m(t[0], Request) && t[0].method ? String(t[0].method).toUpperCase() : t[1] && t[1].method ? String(t[1].method).toUpperCase() : "GET"
    }
    function ft(t) {
        return void 0 === t && (t = []),
        "string" == typeof t[0] ? t[0] : "Request"in nt && m(t[0], Request) ? t[0].url : String(t[0])
    }
    var ct, st;
    function vt(t, n) {
        return void 0 === n && (n = !1),
        function(r) {
            if (r && st !== r && !function(t) {
                if ("keypress" !== t.type)
                    return !1;
                try {
                    var n = t.target;
                    if (!n || !n.tagName)
                        return !0;
                    if ("INPUT" === n.tagName || "TEXTAREA" === n.tagName || n.isContentEditable)
                        return !1
                } catch (t) {}
                return !0
            }(r)) {
                var e = "keypress" === r.type ? "input" : r.type;
                (void 0 === ct || function(t, n) {
                    if (!t)
                        return !0;
                    if (t.type !== n.type)
                        return !0;
                    try {
                        if (t.target !== n.target)
                            return !0
                    } catch (t) {}
                    return !1
                }(st, r)) && (t({
                    event: r,
                    name: e,
                    global: n
                }),
                st = r),
                clearTimeout(ct),
                ct = nt.setTimeout((function() {
                    ct = void 0
                }
                ), 1e3)
            }
        }
    }
    var ht = null;
    var lt, dt = null;
    function yt() {
        var t = g
          , n = t.crypto || t.msCrypto;
        if (n && n.randomUUID)
            return n.randomUUID().replace(/-/g, "");
        var r = n && n.getRandomValues ? function() {
            return n.getRandomValues(new Uint8Array(1))[0]
        }
        : function() {
            return 16 * Math.random()
        }
        ;
        return ([1e7] + 1e3 + 4e3 + 8e3 + 1e11).replace(/[018]/g, (function(t) {
            return (t ^ (15 & r()) >> t / 4).toString(16)
        }
        ))
    }
    function pt(t) {
        return t.exception && t.exception.values ? t.exception.values[0] : void 0
    }
    function mt(t) {
        var n = t.message
          , r = t.event_id;
        if (n)
            return n;
        var e = pt(t);
        return e ? e.type && e.value ? e.type + ": " + e.value : e.type || e.value || r || "<unknown>" : r || "<unknown>"
    }
    function bt(t, n, r) {
        var e = t.exception = t.exception || {}
          , i = e.values = e.values || []
          , o = i[0] = i[0] || {};
        o.value || (o.value = n || ""),
        o.type || (o.type = r || "Error")
    }
    function gt(t, n) {
        var r = pt(t);
        if (r) {
            var i = r.mechanism;
            if (r.mechanism = e(e(e({}, {
                type: "generic",
                handled: !0
            }), i), n),
            n && "data"in n) {
                var o = e(e({}, i && i.data), n.data);
                r.mechanism.data = o
            }
        }
    }
    function wt(t) {
        if (t && t.__sentry_captured__)
            return !0;
        try {
            q(t, "__sentry_captured__", !0)
        } catch (t) {}
        return !1
    }
    function Et(t) {
        return Array.isArray(t) ? t : [t]
    }
    function _t(t, n, r) {
        void 0 === n && (n = 1 / 0),
        void 0 === r && (r = 1 / 0);
        try {
            return kt("", t, n, r)
        } catch (t) {
            return {
                ERROR: "**non-serializable** (" + t + ")"
            }
        }
    }
    function jt(t, n, r) {
        void 0 === n && (n = 3),
        void 0 === r && (r = 102400);
        var e, i = _t(t, n);
        return e = i,
        function(t) {
            return ~-encodeURI(t).split(/%..|./).length
        }(JSON.stringify(e)) > r ? jt(t, n - 1, r) : i
    }
    function kt(t, n, r, e, i) {
        var u, a;
        void 0 === r && (r = 1 / 0),
        void 0 === e && (e = 1 / 0),
        void 0 === i && (u = "function" == typeof WeakSet,
        a = u ? new WeakSet : [],
        i = [function(t) {
            if (u)
                return !!a.has(t) || (a.add(t),
                !1);
            for (var n = 0; n < a.length; n++)
                if (a[n] === t)
                    return !0;
            return a.push(t),
            !1
        }
        , function(t) {
            if (u)
                a.delete(t);
            else
                for (var n = 0; n < a.length; n++)
                    if (a[n] === t) {
                        a.splice(n, 1);
                        break
                    }
        }
        ]);
        var f, c = o(i, 2), s = c[0], v = c[1];
        if (null === n || ["number", "boolean", "string"].includes(typeof n) && ("number" != typeof (f = n) || f == f))
            return n;
        var h = function(t, n) {
            try {
                return "domain" === t && n && "object" == typeof n && n.i ? "[Domain]" : "domainEmitter" === t ? "[DomainEmitter]" : "undefined" != typeof global && n === global ? "[Global]" : "undefined" != typeof window && n === window ? "[Window]" : "undefined" != typeof document && n === document ? "[Document]" : function(t) {
                    return d(t) && "nativeEvent"in t && "preventDefault"in t && "stopPropagation"in t
                }(n) ? "[SyntheticEvent]" : "number" == typeof n && n != n ? "[NaN]" : void 0 === n ? "[undefined]" : "function" == typeof n ? "[Function: " + V(n) + "]" : "symbol" == typeof n ? "[" + String(n) + "]" : "bigint" == typeof n ? "[BigInt: " + String(n) + "]" : "[object " + function(t) {
                    var n = Object.getPrototypeOf(t);
                    return n ? n.constructor.name : "null prototype"
                }(n) + "]"
            } catch (t) {
                return "**non-serializable** (" + t + ")"
            }
        }(t, n);
        if (!h.startsWith("[object "))
            return h;
        if (n.__sentry_skip_normalization__)
            return n;
        if (0 === r)
            return h.replace("object ", "");
        if (s(n))
            return "[Circular ~]";
        var l = n;
        if (l && "function" == typeof l.toJSON)
            try {
                return kt("", l.toJSON(), r - 1, e, i)
            } catch (t) {}
        var y = Array.isArray(n) ? [] : {}
          , p = 0
          , m = P(n);
        for (var b in m)
            if (Object.prototype.hasOwnProperty.call(m, b)) {
                if (p >= e) {
                    y[b] = "[MaxProperties ~]";
                    break
                }
                var g = m[b];
                y[b] = kt(b, g, r - 1, e, i),
                p++
            }
        return v(n),
        y
    }
    function St(t) {
        return new Ot((function(n) {
            n(t)
        }
        ))
    }
    function xt(t) {
        return new Ot((function(n, r) {
            r(t)
        }
        ))
    }
    !function(t) {
        t[t.PENDING = 0] = "PENDING",
        t[t.RESOLVED = 1] = "RESOLVED",
        t[t.REJECTED = 2] = "REJECTED"
    }(lt || (lt = {}));
    var Ot = function() {
        function t(t) {
            var n = this;
            this.o = lt.PENDING,
            this.u = [],
            this.v = function(t) {
                n.h(lt.RESOLVED, t)
            }
            ,
            this.l = function(t) {
                n.h(lt.REJECTED, t)
            }
            ,
            this.h = function(t, r) {
                n.o === lt.PENDING && (p(r) ? r.then(n.v, n.l) : (n.o = t,
                n.p = r,
                n.m()))
            }
            ,
            this.m = function() {
                if (n.o !== lt.PENDING) {
                    var t = n.u.slice();
                    n.u = [],
                    t.forEach((function(t) {
                        t[0] || (n.o === lt.RESOLVED && t[1](n.p),
                        n.o === lt.REJECTED && t[2](n.p),
                        t[0] = !0)
                    }
                    ))
                }
            }
            ;
            try {
                t(this.v, this.l)
            } catch (t) {
                this.l(t)
            }
        }
        return t.prototype.then = function(n, r) {
            var e = this;
            return new t((function(t, i) {
                e.u.push([!1, function(r) {
                    if (n)
                        try {
                            t(n(r))
                        } catch (t) {
                            i(t)
                        }
                    else
                        t(r)
                }
                , function(n) {
                    if (r)
                        try {
                            t(r(n))
                        } catch (t) {
                            i(t)
                        }
                    else
                        i(n)
                }
                ]),
                e.m()
            }
            ))
        }
        ,
        t.prototype.catch = function(t) {
            return this.then((function(t) {
                return t
            }
            ), t)
        }
        ,
        t.prototype.finally = function(n) {
            var r = this;
            return new t((function(t, e) {
                var i, o;
                return r.then((function(t) {
                    o = !1,
                    i = t,
                    n && n()
                }
                ), (function(t) {
                    o = !0,
                    i = t,
                    n && n()
                }
                )).then((function() {
                    o ? e(i) : t(i)
                }
                ))
            }
            ))
        }
        ,
        t
    }();
    function Rt(t) {
        var n = [];
        function r(t) {
            return n.splice(n.indexOf(t), 1)[0]
        }
        return {
            $: n,
            add: function(e) {
                if (!(void 0 === t || n.length < t))
                    return xt(new S("Not adding Promise because buffer limit was reached."));
                var i = e();
                return -1 === n.indexOf(i) && n.push(i),
                i.then((function() {
                    return r(i)
                }
                )).then(null, (function() {
                    return r(i).then(null, (function() {}
                    ))
                }
                )),
                i
            },
            drain: function(t) {
                return new Ot((function(r, e) {
                    var i = n.length;
                    if (!i)
                        return r(!0);
                    var o = setTimeout((function() {
                        t && t > 0 && r(!1)
                    }
                    ), t);
                    n.forEach((function(t) {
                        St(t).then((function() {
                            --i || (clearTimeout(o),
                            r(!0))
                        }
                        ), e)
                    }
                    ))
                }
                ))
            }
        }
    }
    function Tt(t) {
        if (!t)
            return {};
        var n = t.match(/^(([^:/?#]+):)?(\/\/([^/?#]*))?([^?#]*)(\?([^#]*))?(#(.*))?$/);
        if (!n)
            return {};
        var r = n[6] || ""
          , e = n[8] || "";
        return {
            host: n[4],
            path: n[5],
            protocol: n[2],
            relative: n[5] + r + e
        }
    }
    var Dt = ["fatal", "error", "warning", "log", "info", "debug"];
    var Nt = w()
      , At = {
        nowSeconds: function() {
            return Date.now() / 1e3
        }
    };
    var It = function() {
        var t = Nt.performance;
        if (t && t.now)
            return {
                now: function() {
                    return t.now()
                },
                timeOrigin: Date.now() - t.now()
            }
    }()
      , Mt = void 0 === It ? At : {
        nowSeconds: function() {
            return (It.timeOrigin + It.now()) / 1e3
        }
    }
      , Lt = At.nowSeconds.bind(At)
      , Ct = Mt.nowSeconds.bind(Mt);
    function qt(t, n) {
        return void 0 === n && (n = []),
        [t, n]
    }
    function Ut(t, n) {
        var r = o(t, 2);
        return [r[0], u(r[1], [n])]
    }
    function Ht(t, n) {
        t[1].forEach((function(t) {
            var r = t[0].type;
            n(t, r)
        }
        ))
    }
    function Pt(t, n) {
        return (n || new TextEncoder).encode(t)
    }
    function Xt(t, n) {
        var r, e, u = o(t, 2), a = u[0], f = u[1], c = JSON.stringify(a);
        function s(t) {
            "string" == typeof c ? c = "string" == typeof t ? c + t : [Pt(c, n), t] : c.push("string" == typeof t ? Pt(t, n) : t)
        }
        try {
            for (var v = i(f), h = v.next(); !h.done; h = v.next()) {
                var l = o(h.value, 2)
                  , d = l[0]
                  , y = l[1];
                if (s("\n" + JSON.stringify(d) + "\n"),
                "string" == typeof y || y instanceof Uint8Array)
                    s(y);
                else {
                    var p = void 0;
                    try {
                        p = JSON.stringify(y)
                    } catch (t) {
                        p = JSON.stringify(_t(y))
                    }
                    s(p)
                }
            }
        } catch (t) {
            r = {
                error: t
            }
        } finally {
            try {
                h && !h.done && (e = v.return) && e.call(v)
            } finally {
                if (r)
                    throw r.error
            }
        }
        return "string" == typeof c ? c : function(t) {
            var n, r, e = t.reduce((function(t, n) {
                return t + n.length
            }
            ), 0), o = new Uint8Array(e), u = 0;
            try {
                for (var a = i(t), f = a.next(); !f.done; f = a.next()) {
                    var c = f.value;
                    o.set(c, u),
                    u += c.length
                }
            } catch (t) {
                n = {
                    error: t
                }
            } finally {
                try {
                    f && !f.done && (r = a.return) && r.call(a)
                } finally {
                    if (n)
                        throw n.error
                }
            }
            return o
        }(c)
    }
    function $t(t, n) {
        var r = "string" == typeof t.data ? Pt(t.data, n) : t.data;
        return [W({
            type: "attachment",
            length: r.length,
            filename: t.filename,
            content_type: t.contentType,
            attachment_type: t.attachmentType
        }), r]
    }
    !function() {
        var t = Nt.performance;
        if (t && t.now) {
            var n = 36e5
              , r = t.now()
              , e = Date.now()
              , i = t.timeOrigin ? Math.abs(t.timeOrigin + r - e) : n
              , o = i < n
              , u = t.timing && t.timing.navigationStart
              , a = "number" == typeof u ? Math.abs(u + r - e) : n;
            (o || a < n) && (i <= a && t.timeOrigin)
        }
    }();
    var Ft = {
        session: "session",
        sessions: "session",
        attachment: "attachment",
        transaction: "transaction",
        event: "error",
        client_report: "internal",
        user_report: "default",
        profile: "profile",
        replay_event: "replay",
        replay_recording: "replay"
    };
    function Wt(t) {
        return Ft[t]
    }
    function Bt(t) {
        if (t && t.sdk) {
            var n = t.sdk;
            return {
                name: n.name,
                version: n.version
            }
        }
    }
    function Jt(t, n, r) {
        var u, a, f, c, s = n.statusCode, v = n.headers;
        void 0 === r && (r = Date.now());
        var h = e({}, t)
          , l = v && v["x-sentry-rate-limits"]
          , d = v && v["retry-after"];
        if (l)
            try {
                for (var y = i(l.trim().split(",")), p = y.next(); !p.done; p = y.next()) {
                    var m = o(p.value.split(":", 2), 2)
                      , b = m[0]
                      , g = m[1]
                      , w = parseInt(b, 10)
                      , E = 1e3 * (isNaN(w) ? 60 : w);
                    if (g)
                        try {
                            for (var _ = (f = void 0,
                            i(g.split(";"))), j = _.next(); !j.done; j = _.next()) {
                                h[j.value] = r + E
                            }
                        } catch (t) {
                            f = {
                                error: t
                            }
                        } finally {
                            try {
                                j && !j.done && (c = _.return) && c.call(_)
                            } finally {
                                if (f)
                                    throw f.error
                            }
                        }
                    else
                        h.all = r + E
                }
            } catch (t) {
                u = {
                    error: t
                }
            } finally {
                try {
                    p && !p.done && (a = y.return) && a.call(y)
                } finally {
                    if (u)
                        throw u.error
                }
            }
        else
            d ? h.all = r + function(t, n) {
                void 0 === n && (n = Date.now());
                var r = parseInt("" + t, 10);
                if (!isNaN(r))
                    return 1e3 * r;
                var e = Date.parse("" + t);
                return isNaN(e) ? 6e4 : e - n
            }(d, r) : 429 === s && (h.all = r + 6e4);
        return h
    }
    function zt(t) {
        var n = Ct()
          , r = {
            sid: yt(),
            init: !0,
            timestamp: n,
            started: n,
            duration: 0,
            status: "ok",
            errors: 0,
            ignoreDuration: !1,
            toJSON: function() {
                return function(t) {
                    return W({
                        sid: "" + t.sid,
                        init: t.init,
                        started: new Date(1e3 * t.started).toISOString(),
                        timestamp: new Date(1e3 * t.timestamp).toISOString(),
                        status: t.status,
                        errors: t.errors,
                        did: "number" == typeof t.did || "string" == typeof t.did ? "" + t.did : void 0,
                        duration: t.duration,
                        attrs: {
                            release: t.release,
                            environment: t.environment,
                            ip_address: t.ipAddress,
                            user_agent: t.userAgent
                        }
                    })
                }(r)
            }
        };
        return t && Gt(r, t),
        r
    }
    function Gt(t, n) {
        if (void 0 === n && (n = {}),
        n.user && (!t.ipAddress && n.user.ip_address && (t.ipAddress = n.user.ip_address),
        t.did || n.did || (t.did = n.user.id || n.user.email || n.user.username)),
        t.timestamp = n.timestamp || Ct(),
        n.ignoreDuration && (t.ignoreDuration = n.ignoreDuration),
        n.sid && (t.sid = 32 === n.sid.length ? n.sid : yt()),
        void 0 !== n.init && (t.init = n.init),
        !t.did && n.did && (t.did = "" + n.did),
        "number" == typeof n.started && (t.started = n.started),
        t.ignoreDuration)
            t.duration = void 0;
        else if ("number" == typeof n.duration)
            t.duration = n.duration;
        else {
            var r = t.timestamp - t.started;
            t.duration = r >= 0 ? r : 0
        }
        n.release && (t.release = n.release),
        n.environment && (t.environment = n.environment),
        !t.ipAddress && n.ipAddress && (t.ipAddress = n.ipAddress),
        !t.userAgent && n.userAgent && (t.userAgent = n.userAgent),
        "number" == typeof n.errors && (t.errors = n.errors),
        n.status && (t.status = n.status)
    }
    var Kt = function() {
        function t() {
            this.g = !1,
            this._ = [],
            this.j = [],
            this.k = [],
            this.S = [],
            this.O = {},
            this.R = {},
            this.T = {},
            this.D = {},
            this.N = {}
        }
        return t.clone = function(n) {
            var r = new t;
            return n && (r.k = u(n.k),
            r.R = e({}, n.R),
            r.T = e({}, n.T),
            r.D = e({}, n.D),
            r.O = n.O,
            r.A = n.A,
            r.I = n.I,
            r.M = n.M,
            r.L = n.L,
            r.C = n.C,
            r.j = u(n.j),
            r.q = n.q,
            r.S = u(n.S),
            r.N = e({}, n.N)),
            r
        }
        ,
        t.prototype.addScopeListener = function(t) {
            this._.push(t)
        }
        ,
        t.prototype.addEventProcessor = function(t) {
            return this.j.push(t),
            this
        }
        ,
        t.prototype.setUser = function(t) {
            return this.O = t || {},
            this.M && Gt(this.M, {
                user: t
            }),
            this.U(),
            this
        }
        ,
        t.prototype.getUser = function() {
            return this.O
        }
        ,
        t.prototype.getRequestSession = function() {
            return this.q
        }
        ,
        t.prototype.setRequestSession = function(t) {
            return this.q = t,
            this
        }
        ,
        t.prototype.setTags = function(t) {
            return this.R = e(e({}, this.R), t),
            this.U(),
            this
        }
        ,
        t.prototype.setTag = function(t, n) {
            var r;
            return this.R = e(e({}, this.R), ((r = {})[t] = n,
            r)),
            this.U(),
            this
        }
        ,
        t.prototype.setExtras = function(t) {
            return this.T = e(e({}, this.T), t),
            this.U(),
            this
        }
        ,
        t.prototype.setExtra = function(t, n) {
            var r;
            return this.T = e(e({}, this.T), ((r = {})[t] = n,
            r)),
            this.U(),
            this
        }
        ,
        t.prototype.setFingerprint = function(t) {
            return this.C = t,
            this.U(),
            this
        }
        ,
        t.prototype.setLevel = function(t) {
            return this.A = t,
            this.U(),
            this
        }
        ,
        t.prototype.setTransactionName = function(t) {
            return this.L = t,
            this.U(),
            this
        }
        ,
        t.prototype.setContext = function(t, n) {
            return null === n ? delete this.D[t] : this.D[t] = n,
            this.U(),
            this
        }
        ,
        t.prototype.setSpan = function(t) {
            return this.I = t,
            this.U(),
            this
        }
        ,
        t.prototype.getSpan = function() {
            return this.I
        }
        ,
        t.prototype.getTransaction = function() {
            var t = this.getSpan();
            return t && t.transaction
        }
        ,
        t.prototype.setSession = function(t) {
            return t ? this.M = t : delete this.M,
            this.U(),
            this
        }
        ,
        t.prototype.getSession = function() {
            return this.M
        }
        ,
        t.prototype.update = function(n) {
            if (!n)
                return this;
            if ("function" == typeof n) {
                var r = n(this);
                return r instanceof t ? r : this
            }
            return n instanceof t ? (this.R = e(e({}, this.R), n.R),
            this.T = e(e({}, this.T), n.T),
            this.D = e(e({}, this.D), n.D),
            n.O && Object.keys(n.O).length && (this.O = n.O),
            n.A && (this.A = n.A),
            n.C && (this.C = n.C),
            n.q && (this.q = n.q)) : d(n) && (n = n,
            this.R = e(e({}, this.R), n.tags),
            this.T = e(e({}, this.T), n.extra),
            this.D = e(e({}, this.D), n.contexts),
            n.user && (this.O = n.user),
            n.level && (this.A = n.level),
            n.fingerprint && (this.C = n.fingerprint),
            n.requestSession && (this.q = n.requestSession)),
            this
        }
        ,
        t.prototype.clear = function() {
            return this.k = [],
            this.R = {},
            this.T = {},
            this.O = {},
            this.D = {},
            this.A = void 0,
            this.L = void 0,
            this.C = void 0,
            this.q = void 0,
            this.I = void 0,
            this.M = void 0,
            this.U(),
            this.S = [],
            this
        }
        ,
        t.prototype.addBreadcrumb = function(t, n) {
            var r = "number" == typeof n ? n : 100;
            if (r <= 0)
                return this;
            var i = e({
                timestamp: Lt()
            }, t);
            return this.k = u(this.k, [i]).slice(-r),
            this.U(),
            this
        }
        ,
        t.prototype.getLastBreadcrumb = function() {
            return this.k[this.k.length - 1]
        }
        ,
        t.prototype.clearBreadcrumbs = function() {
            return this.k = [],
            this.U(),
            this
        }
        ,
        t.prototype.addAttachment = function(t) {
            return this.S.push(t),
            this
        }
        ,
        t.prototype.getAttachments = function() {
            return this.S
        }
        ,
        t.prototype.clearAttachments = function() {
            return this.S = [],
            this
        }
        ,
        t.prototype.applyToEvent = function(t, n) {
            if (void 0 === n && (n = {}),
            this.T && Object.keys(this.T).length && (t.extra = e(e({}, this.T), t.extra)),
            this.R && Object.keys(this.R).length && (t.tags = e(e({}, this.R), t.tags)),
            this.O && Object.keys(this.O).length && (t.user = e(e({}, this.O), t.user)),
            this.D && Object.keys(this.D).length && (t.contexts = e(e({}, this.D), t.contexts)),
            this.A && (t.level = this.A),
            this.L && (t.transaction = this.L),
            this.I) {
                t.contexts = e({
                    trace: this.I.getTraceContext()
                }, t.contexts);
                var r = this.I.transaction && this.I.transaction.name;
                r && (t.tags = e({
                    transaction: r
                }, t.tags))
            }
            return this.H(t),
            t.breadcrumbs = u(t.breadcrumbs || [], this.k),
            t.breadcrumbs = t.breadcrumbs.length > 0 ? t.breadcrumbs : void 0,
            t.sdkProcessingMetadata = e(e({}, t.sdkProcessingMetadata), this.N),
            this.P(u(Vt(), this.j), t, n)
        }
        ,
        t.prototype.setSDKProcessingMetadata = function(t) {
            return this.N = e(e({}, this.N), t),
            this
        }
        ,
        t.prototype.P = function(t, n, r, i) {
            var o = this;
            return void 0 === i && (i = 0),
            new Ot((function(u, a) {
                var f = t[i];
                if (null === n || "function" != typeof f)
                    u(n);
                else {
                    var c = f(e({}, n), r);
                    p(c) ? c.then((function(n) {
                        return o.P(t, n, r, i + 1).then(u)
                    }
                    )).then(null, a) : o.P(t, c, r, i + 1).then(u).then(null, a)
                }
            }
            ))
        }
        ,
        t.prototype.U = function() {
            var t = this;
            this.g || (this.g = !0,
            this._.forEach((function(n) {
                n(t)
            }
            )),
            this.g = !1)
        }
        ,
        t.prototype.H = function(t) {
            t.fingerprint = t.fingerprint ? Et(t.fingerprint) : [],
            this.C && (t.fingerprint = t.fingerprint.concat(this.C)),
            t.fingerprint && !t.fingerprint.length && delete t.fingerprint
        }
        ,
        t
    }();
    function Vt() {
        return E("globalEventProcessors", (function() {
            return []
        }
        ))
    }
    function Yt(t) {
        Vt().push(t)
    }
    var Qt = function() {
        function t(t, n, r) {
            void 0 === n && (n = new Kt),
            void 0 === r && (r = 4),
            this.X = r,
            this.F = [{}],
            this.getStackTop().scope = n,
            t && this.bindClient(t)
        }
        return t.prototype.isOlderThan = function(t) {
            return this.X < t
        }
        ,
        t.prototype.bindClient = function(t) {
            this.getStackTop().client = t,
            t && t.setupIntegrations && t.setupIntegrations()
        }
        ,
        t.prototype.pushScope = function() {
            var t = Kt.clone(this.getScope());
            return this.getStack().push({
                client: this.getClient(),
                scope: t
            }),
            t
        }
        ,
        t.prototype.popScope = function() {
            return !(this.getStack().length <= 1) && !!this.getStack().pop()
        }
        ,
        t.prototype.withScope = function(t) {
            var n = this.pushScope();
            try {
                t(n)
            } finally {
                this.popScope()
            }
        }
        ,
        t.prototype.getClient = function() {
            return this.getStackTop().client
        }
        ,
        t.prototype.getScope = function() {
            return this.getStackTop().scope
        }
        ,
        t.prototype.getStack = function() {
            return this.F
        }
        ,
        t.prototype.getStackTop = function() {
            return this.F[this.F.length - 1]
        }
        ,
        t.prototype.captureException = function(t, n) {
            var r = this.W = n && n.event_id ? n.event_id : yt()
              , i = new Error("Sentry syntheticException");
            return this.B((function(o, u) {
                o.captureException(t, e(e({
                    originalException: t,
                    syntheticException: i
                }, n), {
                    event_id: r
                }), u)
            }
            )),
            r
        }
        ,
        t.prototype.captureMessage = function(t, n, r) {
            var i = this.W = r && r.event_id ? r.event_id : yt()
              , o = new Error(t);
            return this.B((function(u, a) {
                u.captureMessage(t, n, e(e({
                    originalException: t,
                    syntheticException: o
                }, r), {
                    event_id: i
                }), a)
            }
            )),
            i
        }
        ,
        t.prototype.captureEvent = function(t, n) {
            var r = n && n.event_id ? n.event_id : yt();
            return t.type || (this.W = r),
            this.B((function(i, o) {
                i.captureEvent(t, e(e({}, n), {
                    event_id: r
                }), o)
            }
            )),
            r
        }
        ,
        t.prototype.lastEventId = function() {
            return this.W
        }
        ,
        t.prototype.addBreadcrumb = function(t, n) {
            var r = this.getStackTop()
              , i = r.scope
              , o = r.client;
            if (i && o) {
                var u = o.getOptions && o.getOptions() || {}
                  , a = u.beforeBreadcrumb
                  , f = void 0 === a ? null : a
                  , c = u.maxBreadcrumbs
                  , s = void 0 === c ? 100 : c;
                if (!(s <= 0)) {
                    var v = Lt()
                      , h = e({
                        timestamp: v
                    }, t)
                      , l = f ? function(t) {
                        if (!("console"in g))
                            return t();
                        var n = g.console
                          , r = {};
                        N.forEach((function(t) {
                            var e = n[t] && n[t].__sentry_original__;
                            t in n && e && (r[t] = n[t],
                            n[t] = e)
                        }
                        ));
                        try {
                            return t()
                        } finally {
                            Object.keys(r).forEach((function(t) {
                                n[t] = r[t]
                            }
                            ))
                        }
                    }((function() {
                        return f(h, n)
                    }
                    )) : h;
                    null !== l && i.addBreadcrumb(l, s)
                }
            }
        }
        ,
        t.prototype.setUser = function(t) {
            var n = this.getScope();
            n && n.setUser(t)
        }
        ,
        t.prototype.setTags = function(t) {
            var n = this.getScope();
            n && n.setTags(t)
        }
        ,
        t.prototype.setExtras = function(t) {
            var n = this.getScope();
            n && n.setExtras(t)
        }
        ,
        t.prototype.setTag = function(t, n) {
            var r = this.getScope();
            r && r.setTag(t, n)
        }
        ,
        t.prototype.setExtra = function(t, n) {
            var r = this.getScope();
            r && r.setExtra(t, n)
        }
        ,
        t.prototype.setContext = function(t, n) {
            var r = this.getScope();
            r && r.setContext(t, n)
        }
        ,
        t.prototype.configureScope = function(t) {
            var n = this.getStackTop()
              , r = n.scope
              , e = n.client;
            r && e && t(r)
        }
        ,
        t.prototype.run = function(t) {
            var n = tn(this);
            try {
                t(this)
            } finally {
                tn(n)
            }
        }
        ,
        t.prototype.getIntegration = function(t) {
            var n = this.getClient();
            if (!n)
                return null;
            try {
                return n.getIntegration(t)
            } catch (t) {
                return null
            }
        }
        ,
        t.prototype.startTransaction = function(t, n) {
            return this.J("startTransaction", t, n)
        }
        ,
        t.prototype.traceHeaders = function() {
            return this.J("traceHeaders")
        }
        ,
        t.prototype.captureSession = function(t) {
            if (void 0 === t && (t = !1),
            t)
                return this.endSession();
            this.G()
        }
        ,
        t.prototype.endSession = function() {
            var t = this.getStackTop()
              , n = t && t.scope
              , r = n && n.getSession();
            r && function(t, n) {
                var r = {};
                n ? r = {
                    status: n
                } : "ok" === t.status && (r = {
                    status: "exited"
                }),
                Gt(t, r)
            }(r),
            this.G(),
            n && n.setSession()
        }
        ,
        t.prototype.startSession = function(t) {
            var n = this.getStackTop()
              , r = n.scope
              , i = n.client
              , o = i && i.getOptions() || {}
              , u = o.release
              , a = o.environment
              , f = (g.navigator || {}).userAgent
              , c = zt(e(e(e({
                release: u,
                environment: a
            }, r && {
                user: r.getUser()
            }), f && {
                userAgent: f
            }), t));
            if (r) {
                var s = r.getSession && r.getSession();
                s && "ok" === s.status && Gt(s, {
                    status: "exited"
                }),
                this.endSession(),
                r.setSession(c)
            }
            return c
        }
        ,
        t.prototype.shouldSendDefaultPii = function() {
            var t = this.getClient()
              , n = t && t.getOptions();
            return Boolean(n && n.sendDefaultPii)
        }
        ,
        t.prototype.G = function() {
            var t = this.getStackTop()
              , n = t.scope
              , r = t.client;
            if (n) {
                var e = n.getSession();
                e && r && r.captureSession && r.captureSession(e)
            }
        }
        ,
        t.prototype.B = function(t) {
            var n = this.getStackTop()
              , r = n.scope
              , e = n.client;
            e && t(e, r)
        }
        ,
        t.prototype.J = function(t) {
            for (var n = [], r = 1; r < arguments.length; r++)
                n[r - 1] = arguments[r];
            var e = Zt()
              , i = e.__SENTRY__;
            if (i && i.extensions && "function" == typeof i.extensions[t])
                return i.extensions[t].apply(this, n)
        }
        ,
        t
    }();
    function Zt() {
        return g.__SENTRY__ = g.__SENTRY__ || {
            extensions: {},
            hub: void 0
        },
        g
    }
    function tn(t) {
        var n = Zt()
          , r = rn(n);
        return en(n, t),
        r
    }
    function nn() {
        var t, n = Zt();
        return (t = n) && t.__SENTRY__ && t.__SENTRY__.hub && !rn(n).isOlderThan(4) || en(n, new Qt),
        rn(n)
    }
    function rn(t) {
        return E("hub", (function() {
            return new Qt
        }
        ), t)
    }
    function en(t, n) {
        return !!t && ((t.__SENTRY__ = t.__SENTRY__ || {}).hub = n,
        !0)
    }
    function captureException(t, n) {
        return nn().captureException(t, {
            captureContext: n
        })
    }
    function on(t) {
        nn().withScope(t)
    }
    function un(t) {
        var n = t.protocol ? t.protocol + ":" : ""
          , r = t.port ? ":" + t.port : "";
        return n + "//" + t.host + r + (t.path ? "/" + t.path : "") + "/api/"
    }
    function an(t, n) {
        return r = e({
            sentry_key: t.publicKey,
            sentry_version: "7"
        }, n && {
            sentry_client: n.name + "/" + n.version
        }),
        Object.keys(r).map((function(t) {
            return encodeURIComponent(t) + "=" + encodeURIComponent(r[t])
        }
        )).join("&");
        var r
    }
    function fn(t, n) {
        void 0 === n && (n = {});
        var r = "string" == typeof n ? n : n.tunnel
          , e = "string" != typeof n && n.K ? n.K.sdk : void 0;
        return r || function(t) {
            return "" + un(t) + t.projectId + "/envelope/"
        }(t) + "?" + an(t, e)
    }
    function cn(t, n, r, i) {
        var o = Bt(r)
          , a = t.type && "replay_event" !== t.type ? t.type : "event";
        !function(t, n) {
            n && (t.sdk = t.sdk || {},
            t.sdk.name = t.sdk.name || n.name,
            t.sdk.version = t.sdk.version || n.version,
            t.sdk.integrations = u(t.sdk.integrations || [], n.integrations || []),
            t.sdk.packages = u(t.sdk.packages || [], n.packages || []))
        }(t, r && r.sdk);
        var f = function(t, n, r, i) {
            var o = t.sdkProcessingMetadata && t.sdkProcessingMetadata.dynamicSamplingContext;
            return e(e(e({
                event_id: t.event_id,
                sent_at: (new Date).toISOString()
            }, n && {
                sdk: n
            }), !!r && {
                dsn: O(i)
            }), "transaction" === t.type && o && {
                trace: W(e({}, o))
            })
        }(t, o, i, n);
        return delete t.sdkProcessingMetadata,
        qt(f, [[{
            type: a
        }, t]])
    }
    var sn = [];
    function vn(t) {
        var n = t.defaultIntegrations || []
          , r = t.integrations;
        n.forEach((function(t) {
            t.isDefaultInstance = !0
        }
        ));
        var e = function(t) {
            var n = {};
            return t.forEach((function(t) {
                var r = t.name
                  , e = n[r];
                e && !e.isDefaultInstance && t.isDefaultInstance || (n[r] = t)
            }
            )),
            Object.values(n)
        }(Array.isArray(r) ? u(n, r) : "function" == typeof r ? Et(r(n)) : n)
          , i = e.findIndex((function(t) {
            return "Debug" === t.name
        }
        ));
        if (-1 !== i) {
            var a = o(e.splice(i, 1), 1)[0];
            e.push(a)
        }
        return e
    }
    function hn(t, n) {
        n[t.name] = t,
        -1 === sn.indexOf(t.name) && (t.setupOnce(Yt, nn),
        sn.push(t.name))
    }
    function ln(t, n, r, i) {
        var o = t.normalizeDepth
          , a = void 0 === o ? 3 : o
          , f = t.normalizeMaxBreadth
          , c = void 0 === f ? 1e3 : f
          , s = e(e({}, n), {
            event_id: n.event_id || r.event_id || yt(),
            timestamp: n.timestamp || Lt()
        })
          , v = r.integrations || t.integrations.map((function(t) {
            return t.name
        }
        ));
        !function(t, n) {
            var r = n.environment
              , e = n.release
              , i = n.dist
              , o = n.maxValueLength
              , u = void 0 === o ? 250 : o;
            "environment"in t || (t.environment = "environment"in n ? r : "production");
            void 0 === t.release && void 0 !== e && (t.release = e);
            void 0 === t.dist && void 0 !== i && (t.dist = i);
            t.message && (t.message = A(t.message, u));
            var a = t.exception && t.exception.values && t.exception.values[0];
            a && a.value && (a.value = A(a.value, u));
            var f = t.request;
            f && f.url && (f.url = A(f.url, u))
        }(s, t),
        function(t, n) {
            n.length > 0 && (t.sdk = t.sdk || {},
            t.sdk.integrations = u(t.sdk.integrations || [], n))
        }(s, v);
        var h = i;
        r.captureContext && (h = Kt.clone(h).update(r.captureContext));
        var l = St(s);
        if (h) {
            if (h.getAttachments) {
                var d = u(r.attachments || [], h.getAttachments());
                d.length && (r.attachments = d)
            }
            l = h.applyToEvent(s, r)
        }
        return l.then((function(t) {
            return "number" == typeof a && a > 0 ? function(t, n, r) {
                if (!t)
                    return null;
                var i = e(e(e(e(e({}, t), t.breadcrumbs && {
                    breadcrumbs: t.breadcrumbs.map((function(t) {
                        return e(e({}, t), t.data && {
                            data: _t(t.data, n, r)
                        })
                    }
                    ))
                }), t.user && {
                    user: _t(t.user, n, r)
                }), t.contexts && {
                    contexts: _t(t.contexts, n, r)
                }), t.extra && {
                    extra: _t(t.extra, n, r)
                });
                t.contexts && t.contexts.trace && i.contexts && (i.contexts.trace = t.contexts.trace,
                t.contexts.trace.data && (i.contexts.trace.data = _t(t.contexts.trace.data, n, r)));
                t.spans && (i.spans = t.spans.map((function(t) {
                    return t.data && (t.data = _t(t.data, n, r)),
                    t
                }
                )));
                return i
            }(t, a, c) : t
        }
        ))
    }
    var dn = function() {
        function t(t) {
            if (this._integrations = {},
            this.V = !1,
            this.Y = 0,
            this.Z = {},
            this.tt = t,
            t.dsn) {
                this.nt = T(t.dsn);
                var n = fn(this.nt, t);
                this.rt = t.transport(e(e({
                    recordDroppedEvent: this.recordDroppedEvent.bind(this)
                }, t.transportOptions), {
                    url: n
                }))
            }
        }
        return t.prototype.captureException = function(t, n, r) {
            var e = this;
            if (!wt(t)) {
                var i = n && n.event_id;
                return this.et(this.eventFromException(t, n).then((function(t) {
                    return e.it(t, n, r)
                }
                )).then((function(t) {
                    i = t
                }
                ))),
                i
            }
        }
        ,
        t.prototype.captureMessage = function(t, n, r, e) {
            var i = this
              , o = r && r.event_id
              , u = l(t) ? this.eventFromMessage(String(t), n, r) : this.eventFromException(t, r);
            return this.et(u.then((function(t) {
                return i.it(t, r, e)
            }
            )).then((function(t) {
                o = t
            }
            ))),
            o
        }
        ,
        t.prototype.captureEvent = function(t, n, r) {
            if (!(n && n.originalException && wt(n.originalException))) {
                var e = n && n.event_id;
                return this.et(this.it(t, n, r).then((function(t) {
                    e = t
                }
                ))),
                e
            }
        }
        ,
        t.prototype.captureSession = function(t) {
            this._isEnabled() && ("string" != typeof t.release || (this.sendSession(t),
            Gt(t, {
                init: !1
            })))
        }
        ,
        t.prototype.getDsn = function() {
            return this.nt
        }
        ,
        t.prototype.getOptions = function() {
            return this.tt
        }
        ,
        t.prototype.getSdkMetadata = function() {
            return this.tt.K
        }
        ,
        t.prototype.getTransport = function() {
            return this.rt
        }
        ,
        t.prototype.flush = function(t) {
            var n = this.rt;
            return n ? this.ot(t).then((function(r) {
                return n.flush(t).then((function(t) {
                    return r && t
                }
                ))
            }
            )) : St(!0)
        }
        ,
        t.prototype.close = function(t) {
            var n = this;
            return this.flush(t).then((function(t) {
                return n.getOptions().enabled = !1,
                t
            }
            ))
        }
        ,
        t.prototype.setupIntegrations = function() {
            var t, n;
            this._isEnabled() && !this.V && (this._integrations = (t = this.tt.integrations,
            n = {},
            t.forEach((function(t) {
                t && hn(t, n)
            }
            )),
            n),
            this.V = !0)
        }
        ,
        t.prototype.getIntegrationById = function(t) {
            return this._integrations[t]
        }
        ,
        t.prototype.getIntegration = function(t) {
            try {
                return this._integrations[t.id] || null
            } catch (t) {
                return null
            }
        }
        ,
        t.prototype.addIntegration = function(t) {
            hn(t, this._integrations)
        }
        ,
        t.prototype.sendEvent = function(t, n) {
            var r, e;
            if (void 0 === n && (n = {}),
            this.nt) {
                var o = cn(t, this.nt, this.tt.K, this.tt.tunnel);
                try {
                    for (var u = i(n.attachments || []), a = u.next(); !a.done; a = u.next()) {
                        o = Ut(o, $t(a.value, this.tt.transportOptions && this.tt.transportOptions.textEncoder))
                    }
                } catch (t) {
                    r = {
                        error: t
                    }
                } finally {
                    try {
                        a && !a.done && (e = u.return) && e.call(u)
                    } finally {
                        if (r)
                            throw r.error
                    }
                }
                this.ut(o)
            }
        }
        ,
        t.prototype.sendSession = function(t) {
            if (this.nt) {
                var n = function(t, n, r, i) {
                    var o = Bt(r);
                    return qt(e(e({
                        sent_at: (new Date).toISOString()
                    }, o && {
                        sdk: o
                    }), !!i && {
                        dsn: O(n)
                    }), ["aggregates"in t ? [{
                        type: "sessions"
                    }, t] : [{
                        type: "session"
                    }, t]])
                }(t, this.nt, this.tt.K, this.tt.tunnel);
                this.ut(n)
            }
        }
        ,
        t.prototype.recordDroppedEvent = function(t, n, r) {
            if (this.tt.sendClientReports) {
                var e = t + ":" + n;
                this.Z[e] = this.Z[e] + 1 || 1
            }
        }
        ,
        t.prototype.ft = function(t, n) {
            var r, o, u = !1, a = !1, f = n.exception && n.exception.values;
            if (f) {
                a = !0;
                try {
                    for (var c = i(f), s = c.next(); !s.done; s = c.next()) {
                        var v = s.value.mechanism;
                        if (v && !1 === v.handled) {
                            u = !0;
                            break
                        }
                    }
                } catch (t) {
                    r = {
                        error: t
                    }
                } finally {
                    try {
                        s && !s.done && (o = c.return) && o.call(c)
                    } finally {
                        if (r)
                            throw r.error
                    }
                }
            }
            var h = "ok" === t.status;
            (h && 0 === t.errors || h && u) && (Gt(t, e(e({}, u && {
                status: "crashed"
            }), {
                errors: t.errors || Number(a || u)
            })),
            this.captureSession(t))
        }
        ,
        t.prototype.ot = function(t) {
            var n = this;
            return new Ot((function(r) {
                var e = 0
                  , i = setInterval((function() {
                    0 == n.Y ? (clearInterval(i),
                    r(!0)) : (e += 1,
                    t && e >= t && (clearInterval(i),
                    r(!1)))
                }
                ), 1)
            }
            ))
        }
        ,
        t.prototype._isEnabled = function() {
            return !1 !== this.getOptions().enabled && void 0 !== this.nt
        }
        ,
        t.prototype.ct = function(t, n, r) {
            var e = this.getOptions()
              , i = Object.keys(this._integrations);
            return !n.integrations && i.length > 0 && (n.integrations = i),
            ln(e, t, n, r)
        }
        ,
        t.prototype.it = function(t, n, r) {
            return void 0 === n && (n = {}),
            this.st(t, n, r).then((function(t) {
                return t.event_id
            }
            ), (function(t) {}
            ))
        }
        ,
        t.prototype.st = function(t, n, r) {
            var i = this
              , o = this.getOptions()
              , u = o.sampleRate;
            if (!this._isEnabled())
                return xt(new S("SDK not enabled, will not capture event.","log"));
            var a = pn(t)
              , f = yn(t)
              , c = t.type || "error"
              , s = "before send for type `" + c + "`";
            if (f && "number" == typeof u && Math.random() > u)
                return this.recordDroppedEvent("sample_rate", "error", t),
                xt(new S("Discarding event because it's not included in the random sample (sampling rate = " + u + ")","log"));
            var v = "replay_event" === c ? "replay" : c;
            return this.ct(t, n, r).then((function(r) {
                if (null === r)
                    throw i.recordDroppedEvent("event_processor", v, t),
                    new S("An event processor returned `null`, will not send event.","log");
                if (n.data && !0 === n.data.__sentry__)
                    return r;
                var e = function(t, n, r) {
                    var e = t.beforeSend
                      , i = t.beforeSendTransaction;
                    if (yn(n) && e)
                        return e(n, r);
                    if (pn(n) && i)
                        return i(n, r);
                    return n
                }(o, r, n);
                return function(t, n) {
                    var r = n + " must return `null` or a valid event.";
                    if (p(t))
                        return t.then((function(t) {
                            if (!d(t) && null !== t)
                                throw new S(r);
                            return t
                        }
                        ), (function(t) {
                            throw new S(n + " rejected with " + t)
                        }
                        ));
                    if (!d(t) && null !== t)
                        throw new S(r);
                    return t
                }(e, s)
            }
            )).then((function(o) {
                if (null === o)
                    throw i.recordDroppedEvent("before_send", v, t),
                    new S(s + " returned `null`, will not send event.","log");
                var u = r && r.getSession();
                !a && u && i.ft(u, o);
                var f = o.transaction_info;
                if (a && f && o.transaction !== t.transaction) {
                    o.transaction_info = e(e({}, f), {
                        source: "custom"
                    })
                }
                return i.sendEvent(o, n),
                o
            }
            )).then(null, (function(t) {
                if (t instanceof S)
                    throw t;
                throw i.captureException(t, {
                    data: {
                        __sentry__: !0
                    },
                    originalException: t
                }),
                new S("Event processing pipeline threw an error, original event will not be sent. Details have been sent as a new event.\nReason: " + t)
            }
            ))
        }
        ,
        t.prototype.et = function(t) {
            var n = this;
            this.Y++,
            t.then((function(t) {
                return n.Y--,
                t
            }
            ), (function(t) {
                return n.Y--,
                t
            }
            ))
        }
        ,
        t.prototype.ut = function(t) {
            this.rt && this.nt && this.rt.send(t).then(null, (function(t) {}
            ))
        }
        ,
        t.prototype.vt = function() {
            var t = this.Z;
            return this.Z = {},
            Object.keys(t).map((function(n) {
                var r = o(n.split(":"), 2);
                return {
                    reason: r[0],
                    category: r[1],
                    quantity: t[n]
                }
            }
            ))
        }
        ,
        t
    }();
    function yn(t) {
        return void 0 === t.type
    }
    function pn(t) {
        return "transaction" === t.type
    }
    function mn(t, n, r) {
        void 0 === r && (r = Rt(t.bufferSize || 30));
        var e = {};
        return {
            send: function(i) {
                var o = [];
                if (Ht(i, (function(n, r) {
                    var i, u, a, f = Wt(r);
                    if (i = e,
                    u = f,
                    void 0 === a && (a = Date.now()),
                    function(t, n) {
                        return t[n] || t.all || 0
                    }(i, u) > a) {
                        var c = bn(n, r);
                        t.recordDroppedEvent("ratelimit_backoff", f, c)
                    } else
                        o.push(n)
                }
                )),
                0 === o.length)
                    return St();
                var u = qt(i[0], o)
                  , a = function(n) {
                    Ht(u, (function(r, e) {
                        var i = bn(r, e);
                        t.recordDroppedEvent(n, Wt(e), i)
                    }
                    ))
                };
                return r.add((function() {
                    return n({
                        body: Xt(u, t.textEncoder)
                    }).then((function(t) {
                        return e = Jt(e, t),
                        t
                    }
                    ), (function(t) {
                        throw a("network_error"),
                        t
                    }
                    ))
                }
                )).then((function(t) {
                    return t
                }
                ), (function(t) {
                    if (t instanceof S)
                        return a("queue_overflow"),
                        St();
                    throw t
                }
                ))
            },
            flush: function(t) {
                return r.drain(t)
            }
        }
    }
    function bn(t, n) {
        if ("event" === n || "transaction" === n)
            return Array.isArray(t) ? t[1] : void 0
    }
    var gn, wn = "7.38.0", En = function() {
        function t() {
            this.name = t.id
        }
        return t.prototype.setupOnce = function() {
            gn = Function.prototype.toString,
            Function.prototype.toString = function() {
                for (var t = [], n = 0; n < arguments.length; n++)
                    t[n] = arguments[n];
                var r = H(this) || this;
                return gn.apply(r, t)
            }
        }
        ,
        t.id = "FunctionToString",
        t
    }(), _n = [/^Script error\.?$/, /^Javascript error: Script error\.? on line 0$/], jn = function() {
        function t(n) {
            void 0 === n && (n = {}),
            this.tt = n,
            this.name = t.id
        }
        return t.prototype.setupOnce = function(n, r) {
            var e = function(n) {
                var e = r();
                if (e) {
                    var i = e.getIntegration(t);
                    if (i) {
                        var o = e.getClient()
                          , a = o ? o.getOptions() : {}
                          , f = function(t, n) {
                            void 0 === t && (t = {});
                            void 0 === n && (n = {});
                            return {
                                allowUrls: u(t.allowUrls || [], n.allowUrls || []),
                                denyUrls: u(t.denyUrls || [], n.denyUrls || []),
                                ignoreErrors: u(t.ignoreErrors || [], n.ignoreErrors || [], _n),
                                ignoreInternal: void 0 === t.ignoreInternal || t.ignoreInternal
                            }
                        }(i.tt, a);
                        return function(t, n) {
                            if (n.ignoreInternal && function(t) {
                                try {
                                    return "SentryError" === t.exception.values[0].type
                                } catch (t) {}
                                return !1
                            }(t))
                                return !0;
                            if (function(t, n) {
                                if (!n || !n.length)
                                    return !1;
                                return function(t) {
                                    if (t.message)
                                        return [t.message];
                                    if (t.exception)
                                        try {
                                            var n = t.exception.values && t.exception.values[0] || {}
                                              , r = n.type
                                              , e = void 0 === r ? "" : r
                                              , i = n.value
                                              , o = void 0 === i ? "" : i;
                                            return ["" + o, e + ": " + o]
                                        } catch (t) {
                                            return []
                                        }
                                    return []
                                }(t).some((function(t) {
                                    return L(t, n)
                                }
                                ))
                            }(t, n.ignoreErrors))
                                return !0;
                            if (function(t, n) {
                                if (!n || !n.length)
                                    return !1;
                                var r = kn(t);
                                return !!r && L(r, n)
                            }(t, n.denyUrls))
                                return !0;
                            if (!function(t, n) {
                                if (!n || !n.length)
                                    return !0;
                                var r = kn(t);
                                return !r || L(r, n)
                            }(t, n.allowUrls))
                                return !0;
                            return !1
                        }(n, f) ? null : n
                    }
                }
                return n
            };
            e.id = this.name,
            n(e)
        }
        ,
        t.id = "InboundFilters",
        t
    }();
    function kn(t) {
        try {
            var n;
            try {
                n = t.exception.values[0].stacktrace.frames
            } catch (t) {}
            return n ? function(t) {
                void 0 === t && (t = []);
                for (var n = t.length - 1; n >= 0; n--) {
                    var r = t[n];
                    if (r && "<anonymous>" !== r.filename && "[native code]" !== r.filename)
                        return r.filename || null
                }
                return null
            }(n) : null
        } catch (t) {
            return null
        }
    }
    var Sn = Object.freeze({
        __proto__: null,
        FunctionToString: En,
        InboundFilters: jn
    })
      , xn = g
      , On = 0;
    function Rn() {
        return On > 0
    }
    function Tn() {
        On++,
        setTimeout((function() {
            On--
        }
        ))
    }
    function Dn(t, n, r) {
        if (void 0 === n && (n = {}),
        "function" != typeof t)
            return t;
        try {
            var i = t.__sentry_wrapped__;
            if (i)
                return i;
            if (H(t))
                return t
        } catch (n) {
            return t
        }
        var sentryWrapped = function() {
            var i = Array.prototype.slice.call(arguments);
            try {
                r && "function" == typeof r && r.apply(this, arguments);
                var o = i.map((function(t) {
                    return Dn(t, n)
                }
                ));
                return t.apply(this, o)
            } catch (t) {
                throw Tn(),
                on((function(r) {
                    r.addEventProcessor((function(t) {
                        return n.mechanism && (bt(t, void 0, void 0),
                        gt(t, n.mechanism)),
                        t.extra = e(e({}, t.extra), {
                            arguments: i
                        }),
                        t
                    }
                    )),
                    captureException(t)
                }
                )),
                t
            }
        };
        try {
            for (var o in t)
                Object.prototype.hasOwnProperty.call(t, o) && (sentryWrapped[o] = t[o])
        } catch (t) {}
        U(sentryWrapped, t),
        q(t, "__sentry_wrapped__", sentryWrapped);
        try {
            Object.getOwnPropertyDescriptor(sentryWrapped, "name").configurable && Object.defineProperty(sentryWrapped, "name", {
                get: function() {
                    return t.name
                }
            })
        } catch (t) {}
        return sentryWrapped
    }
    function Nn(t, n) {
        var r = In(t, n)
          , e = {
            type: n && n.name,
            value: Ln(n)
        };
        return r.length && (e.stacktrace = {
            frames: r
        }),
        void 0 === e.type && "" === e.value && (e.value = "Unrecoverable error caught"),
        e
    }
    function An(t, n) {
        return {
            exception: {
                values: [Nn(t, n)]
            }
        }
    }
    function In(t, n) {
        var r = n.stacktrace || n.stack || ""
          , e = function(t) {
            if (t) {
                if ("number" == typeof t.framesToPop)
                    return t.framesToPop;
                if (Mn.test(t.message))
                    return 1
            }
            return 0
        }(n);
        try {
            return t(r, e)
        } catch (t) {}
        return []
    }
    var Mn = /Minified React error #\d+;/i;
    function Ln(t) {
        var n = t && t.message;
        return n ? n.error && "string" == typeof n.error.message ? n.error.message : n : "No error message"
    }
    function Cn(t, n, r, e) {
        var i = Un(t, n, r && r.syntheticException || void 0, e);
        return gt(i),
        i.level = "error",
        r && r.event_id && (i.event_id = r.event_id),
        St(i)
    }
    function qn(t, n, r, e, i) {
        void 0 === r && (r = "info");
        var o = Hn(t, n, e && e.syntheticException || void 0, i);
        return o.level = r,
        e && e.event_id && (o.event_id = e.event_id),
        St(o)
    }
    function Un(t, n, r, i, o) {
        var u;
        if (s(n) && n.error)
            return An(t, n.error);
        if (v(n) || c(n, "DOMException")) {
            var a = n;
            if ("stack"in n)
                u = An(t, n);
            else {
                var h = a.name || (v(a) ? "DOMError" : "DOMException")
                  , l = a.message ? h + ": " + a.message : h;
                bt(u = Hn(t, l, r, i), l)
            }
            return "code"in a && (u.tags = e(e({}, u.tags), {
                "DOMException.code": "" + a.code
            })),
            u
        }
        return f(n) ? An(t, n) : d(n) || y(n) ? (u = function(t, n, r, e) {
            var i = nn().getClient()
              , o = i && i.getOptions().normalizeDepth
              , u = {
                exception: {
                    values: [{
                        type: y(n) ? n.constructor.name : e ? "UnhandledRejection" : "Error",
                        value: "Non-Error " + (e ? "promise rejection" : "exception") + " captured with keys: " + F(n)
                    }]
                },
                extra: {
                    __serialized__: jt(n, o)
                }
            };
            if (r) {
                var a = In(t, r);
                a.length && (u.exception.values[0].stacktrace = {
                    frames: a
                })
            }
            return u
        }(t, n, r, o),
        gt(u, {
            synthetic: !0
        }),
        u) : (bt(u = Hn(t, n, r, i), "" + n, void 0),
        gt(u, {
            synthetic: !0
        }),
        u)
    }
    function Hn(t, n, r, e) {
        var i = {
            message: n
        };
        if (e && r) {
            var o = In(t, r);
            o.length && (i.exception = {
                values: [{
                    value: n,
                    stacktrace: {
                        frames: o
                    }
                }]
            })
        }
        return i
    }
    var Pn = 1024
      , Xn = "Breadcrumbs"
      , $n = function() {
        function t(n) {
            this.name = t.id,
            this.options = e({
                console: !0,
                dom: !0,
                fetch: !0,
                history: !0,
                sentry: !0,
                xhr: !0
            }, n)
        }
        return t.prototype.setupOnce = function() {
            this.options.console && ot("console", Fn),
            this.options.dom && ot("dom", function(t) {
                function n(n) {
                    var r, e = "object" == typeof t ? t.serializeAttribute : void 0, i = "object" == typeof t && "number" == typeof t.maxStringLength ? t.maxStringLength : void 0;
                    i && i > Pn && (i = Pn),
                    "string" == typeof e && (e = [e]);
                    try {
                        r = n.event.target ? j(n.event.target, {
                            keyAttrs: e,
                            maxStringLength: i
                        }) : j(n.event, {
                            keyAttrs: e,
                            maxStringLength: i
                        })
                    } catch (t) {
                        r = "<unknown>"
                    }
                    0 !== r.length && nn().addBreadcrumb({
                        category: "ui." + n.name,
                        message: r
                    }, {
                        event: n.event,
                        name: n.name,
                        global: n.global
                    })
                }
                return n
            }(this.options.dom)),
            this.options.xhr && ot("xhr", Wn),
            this.options.fetch && ot("fetch", Bn),
            this.options.history && ot("history", Jn)
        }
        ,
        t.prototype.addSentryBreadcrumb = function(t) {
            this.options.sentry && nn().addBreadcrumb({
                category: "sentry." + ("transaction" === t.type ? "transaction" : "event"),
                event_id: t.event_id,
                level: t.level,
                message: mt(t)
            }, {
                event: t
            })
        }
        ,
        t.id = Xn,
        t
    }();
    function Fn(t) {
        for (var n = 0; n < t.args.length; n++)
            if ("ref=Ref<" === t.args[n]) {
                t.args[n + 1] = "viewRef";
                break
            }
        var r, e = {
            category: "console",
            data: {
                arguments: t.args,
                logger: "console"
            },
            level: (r = t.level,
            "warn" === r ? "warning" : Dt.includes(r) ? r : "log"),
            message: I(t.args, " ")
        };
        if ("assert" === t.level) {
            if (!1 !== t.args[0])
                return;
            e.message = "Assertion failed: " + (I(t.args.slice(1), " ") || "console.assert"),
            e.data.arguments = t.args.slice(1)
        }
        nn().addBreadcrumb(e, {
            input: t.args,
            level: t.level
        })
    }
    function Wn(t) {
        if (t.endTimestamp) {
            if (t.xhr.__sentry_own_request__)
                return;
            var n = t.xhr.__sentry_xhr__ || {}
              , r = n.method
              , e = n.url
              , i = n.status_code
              , o = n.body;
            nn().addBreadcrumb({
                category: "xhr",
                data: {
                    method: r,
                    url: e,
                    status_code: i
                },
                type: "http"
            }, {
                xhr: t.xhr,
                input: o
            })
        } else
            ;
    }
    function Bn(t) {
        t.endTimestamp && (t.fetchData.url.match(/sentry_key/) && "POST" === t.fetchData.method || (t.error ? nn().addBreadcrumb({
            category: "fetch",
            data: t.fetchData,
            level: "error",
            type: "http"
        }, {
            data: t.error,
            input: t.args
        }) : nn().addBreadcrumb({
            category: "fetch",
            data: e(e({}, t.fetchData), {
                status_code: t.response.status
            }),
            type: "http"
        }, {
            input: t.args,
            response: t.response
        })))
    }
    function Jn(t) {
        var n = t.from
          , r = t.to
          , e = Tt(xn.location.href)
          , i = Tt(n)
          , o = Tt(r);
        i.path || (i = e),
        e.protocol === o.protocol && e.host === o.host && (r = o.relative),
        e.protocol === i.protocol && e.host === i.host && (n = i.relative),
        nn().addBreadcrumb({
            category: "navigation",
            data: {
                from: n,
                to: r
            }
        })
    }
    var zn = function(t) {
        function n(n) {
            var r = this
              , e = xn.SENTRY_SDK_SOURCE || "cdn";
            return n.K = n.K || {},
            n.K.sdk = n.K.sdk || {
                name: "sentry.javascript.browser",
                packages: [{
                    name: e + ":@sentry/browser",
                    version: wn
                }],
                version: wn
            },
            r = t.call(this, n) || this,
            n.sendClientReports && xn.document && xn.document.addEventListener("visibilitychange", (function() {
                "hidden" === xn.document.visibilityState && r.ht()
            }
            )),
            r
        }
        return r(n, t),
        n.prototype.eventFromException = function(t, n) {
            return Cn(this.tt.stackParser, t, n, this.tt.attachStacktrace)
        }
        ,
        n.prototype.eventFromMessage = function(t, n, r) {
            return void 0 === n && (n = "info"),
            qn(this.tt.stackParser, t, n, r, this.tt.attachStacktrace)
        }
        ,
        n.prototype.sendEvent = function(n, r) {
            var e = this.getIntegrationById(Xn);
            e && e.addSentryBreadcrumb && e.addSentryBreadcrumb(n),
            t.prototype.sendEvent.call(this, n, r)
        }
        ,
        n.prototype.ct = function(n, r, e) {
            return n.platform = n.platform || "javascript",
            t.prototype.ct.call(this, n, r, e)
        }
        ,
        n.prototype.ht = function() {
            var t = this.vt();
            if (0 !== t.length && this.nt) {
                var n, r, e, i = fn(this.nt, this.tt), o = (n = t,
                qt((r = this.tt.tunnel && O(this.nt)) ? {
                    dsn: r
                } : {}, [[{
                    type: "client_report"
                }, {
                    timestamp: e || Lt(),
                    discarded_events: n
                }]]));
                try {
                    if ("[object Navigator]" === Object.prototype.toString.call(xn && xn.navigator) && "function" == typeof xn.navigator.sendBeacon && !this.tt.transportOptions)
                        xn.navigator.sendBeacon.bind(xn.navigator)(i, Xt(o));
                    else
                        this.ut(o)
                } catch (t) {}
            }
        }
        ,
        n
    }(dn)
      , Gn = void 0;
    function Kn(t, n) {
        return void 0 === n && (n = function() {
            if (Gn)
                return Gn;
            if (Z(xn.fetch))
                return Gn = xn.fetch.bind(xn);
            var t = xn.document
              , n = xn.fetch;
            if (t && "function" == typeof t.createElement)
                try {
                    var r = t.createElement("iframe");
                    r.hidden = !0,
                    t.head.appendChild(r);
                    var e = r.contentWindow;
                    e && e.fetch && (n = e.fetch),
                    t.head.removeChild(r)
                } catch (t) {}
            return Gn = n.bind(xn)
        }()),
        mn(t, (function(r) {
            var i = e({
                body: r.body,
                method: "POST",
                referrerPolicy: "origin",
                headers: t.headers,
                keepalive: r.body.length <= 65536
            }, t.fetchOptions);
            try {
                return n(t.url, i).then((function(t) {
                    return {
                        statusCode: t.status,
                        headers: {
                            "x-sentry-rate-limits": t.headers.get("X-Sentry-Rate-Limits"),
                            "retry-after": t.headers.get("Retry-After")
                        }
                    }
                }
                ))
            } catch (t) {
                return Gn = void 0,
                xt(t)
            }
        }
        ))
    }
    function Vn(t) {
        return mn(t, (function(n) {
            return new Ot((function(r, e) {
                var i = new XMLHttpRequest;
                for (var o in i.onerror = e,
                i.onreadystatechange = function() {
                    4 === i.readyState && r({
                        statusCode: i.status,
                        headers: {
                            "x-sentry-rate-limits": i.getResponseHeader("X-Sentry-Rate-Limits"),
                            "retry-after": i.getResponseHeader("Retry-After")
                        }
                    })
                }
                ,
                i.open("POST", t.url),
                t.headers)
                    Object.prototype.hasOwnProperty.call(t.headers, o) && i.setRequestHeader(o, t.headers[o]);
                i.send(n.body)
            }
            ))
        }
        ))
    }
    var Yn = "?";
    function Qn(t, n, r, e) {
        var i = {
            filename: t,
            abs_path: t,
            function: n,
            in_app: !0
        };
        return void 0 !== r && (i.lineno = r),
        void 0 !== e && (i.colno = e),
        i
    }
    var Zn = /^\s*at (?:(.*\).*?|.*?) ?\((?:address at )?)?(?:async )?((?:file|https?|blob|chrome-extension|address|native|eval|webpack|<anonymous>|[-a-z]+:|.*bundle|\/)?.*?)(?::(\d+))?(?::(\d+))?\)?\s*$/i
      , tr = /\((\S*)(?::(\d+))(?::(\d+))\)/
      , nr = [30, function(t) {
        var n = Zn.exec(t);
        if (n) {
            if (n[2] && 0 === n[2].indexOf("eval")) {
                var r = tr.exec(n[2]);
                r && (n[2] = r[1],
                n[3] = r[2],
                n[4] = r[3])
            }
            var e = o(lr(n[1] || Yn, n[2]), 2)
              , i = e[0];
            return Qn(e[1], i, n[3] ? +n[3] : void 0, n[4] ? +n[4] : void 0)
        }
    }
    ]
      , rr = /^\s*(.*?)(?:\((.*?)\))?(?:^|@)?((?:file|https?|blob|chrome|webpack|resource|moz-extension|safari-extension|safari-web-extension|capacitor)?:\/.*?|\[native code\]|[^@]*(?:bundle|\d+\.js)|\/[\w\-. /=]+)(?::(\d+))?(?::(\d+))?\s*$/i
      , er = /(\S+) line (\d+)(?: > eval line \d+)* > eval/i
      , ir = [50, function(t) {
        var n, r = rr.exec(t);
        if (r) {
            if (r[3] && r[3].indexOf(" > eval") > -1) {
                var e = er.exec(r[3]);
                e && (r[1] = r[1] || "eval",
                r[3] = e[1],
                r[4] = e[2],
                r[5] = "")
            }
            var i = r[3]
              , u = r[1] || Yn;
            return u = (n = o(lr(u, i), 2))[0],
            Qn(i = n[1], u, r[4] ? +r[4] : void 0, r[5] ? +r[5] : void 0)
        }
    }
    ]
      , or = /^\s*at (?:((?:\[object object\])?.+) )?\(?((?:file|ms-appx|https?|webpack|blob):.*?):(\d+)(?::(\d+))?\)?\s*$/i
      , ur = [40, function(t) {
        var n = or.exec(t);
        return n ? Qn(n[2], n[1] || Yn, +n[3], n[4] ? +n[4] : void 0) : void 0
    }
    ]
      , ar = / line (\d+).*script (?:in )?(\S+)(?:: in function (\S+))?$/i
      , fr = [10, function(t) {
        var n = ar.exec(t);
        return n ? Qn(n[2], n[3] || Yn, +n[1]) : void 0
    }
    ]
      , cr = / line (\d+), column (\d+)\s*(?:in (?:<anonymous function: ([^>]+)>|([^)]+))\(.*\))? in (.*):\s*$/i
      , sr = [20, function(t) {
        var n = cr.exec(t);
        return n ? Qn(n[5], n[3] || n[4] || Yn, +n[1], +n[2]) : void 0
    }
    ]
      , vr = [nr, ir, ur]
      , hr = z.apply(void 0, u(vr))
      , lr = function(t, n) {
        var r = -1 !== t.indexOf("safari-extension")
          , e = -1 !== t.indexOf("safari-web-extension");
        return r || e ? [-1 !== t.indexOf("@") ? t.split("@")[0] : Yn, r ? "safari-extension:" + n : "safari-web-extension:" + n] : [t, n]
    }
      , dr = function() {
        function t(n) {
            this.name = t.id,
            this.lt = {
                onerror: yr,
                onunhandledrejection: pr
            },
            this.tt = e({
                onerror: !0,
                onunhandledrejection: !0
            }, n)
        }
        return t.prototype.setupOnce = function() {
            Error.stackTraceLimit = 50;
            var t = this.tt;
            for (var n in t) {
                var r = this.lt[n];
                r && t[n] && (r(),
                this.lt[n] = void 0)
            }
        }
        ,
        t.id = "GlobalHandlers",
        t
    }();
    function yr() {
        ot("error", (function(t) {
            var n = o(gr(), 3)
              , r = n[0]
              , e = n[1]
              , i = n[2];
            if (r.getIntegration(dr)) {
                var u = t.msg
                  , a = t.url
                  , f = t.line
                  , c = t.column
                  , v = t.error;
                if (!(Rn() || v && v.__sentry_own_request__)) {
                    var l = void 0 === v && h(u) ? function(t, n, r, e) {
                        var i = /^(?:[Uu]ncaught (?:exception: )?)?(?:((?:Eval|Internal|Range|Reference|Syntax|Type|URI|)Error): )?(.*)$/i
                          , o = s(t) ? t.message : t
                          , u = "Error"
                          , a = o.match(i);
                        a && (u = a[1],
                        o = a[2]);
                        return mr({
                            exception: {
                                values: [{
                                    type: u,
                                    value: o
                                }]
                            }
                        }, n, r, e)
                    }(u, a, f, c) : mr(Un(e, v || u, void 0, i, !1), a, f, c);
                    l.level = "error",
                    br(r, v, l, "onerror")
                }
            }
        }
        ))
    }
    function pr() {
        ot("unhandledrejection", (function(t) {
            var n = o(gr(), 3)
              , r = n[0]
              , e = n[1]
              , i = n[2];
            if (r.getIntegration(dr)) {
                var u = t;
                try {
                    "reason"in t ? u = t.reason : "detail"in t && "reason"in t.detail && (u = t.detail.reason)
                } catch (t) {}
                if (Rn() || u && u.__sentry_own_request__)
                    return !0;
                var a = l(u) ? {
                    exception: {
                        values: [{
                            type: "UnhandledRejection",
                            value: "Non-Error promise rejection captured with value: " + String(u)
                        }]
                    }
                } : Un(e, u, void 0, i, !0);
                a.level = "error",
                br(r, u, a, "onunhandledrejection")
            }
        }
        ))
    }
    function mr(t, n, r, e) {
        var i = t.exception = t.exception || {}
          , o = i.values = i.values || []
          , u = o[0] = o[0] || {}
          , a = u.stacktrace = u.stacktrace || {}
          , f = a.frames = a.frames || []
          , c = isNaN(parseInt(e, 10)) ? void 0 : e
          , s = isNaN(parseInt(r, 10)) ? void 0 : r
          , v = h(n) && n.length > 0 ? n : function() {
            try {
                return _.document.location.href
            } catch (t) {
                return ""
            }
        }();
        return 0 === f.length && f.push({
            colno: c,
            filename: v,
            function: "?",
            in_app: !0,
            lineno: s
        }),
        t
    }
    function br(t, n, r, e) {
        gt(r, {
            handled: !1,
            type: e
        }),
        t.captureEvent(r, {
            originalException: n
        })
    }
    function gr() {
        var t = nn()
          , n = t.getClient()
          , r = n && n.getOptions() || {
            stackParser: function() {
                return []
            },
            attachStacktrace: !1
        };
        return [t, r.stackParser, r.attachStacktrace]
    }
    var wr = ["EventTarget", "Window", "Node", "ApplicationCache", "AudioTrackList", "ChannelMergerNode", "CryptoOperation", "EventSource", "FileReader", "HTMLUnknownElement", "IDBDatabase", "IDBRequest", "IDBTransaction", "KeyOperation", "MediaController", "MessagePort", "ModalWindow", "Notification", "SVGElementInstance", "Screen", "TextTrack", "TextTrackCue", "TextTrackList", "WebSocket", "WebSocketWorker", "Worker", "XMLHttpRequest", "XMLHttpRequestEventTarget", "XMLHttpRequestUpload"]
      , Er = function() {
        function t(n) {
            this.name = t.id,
            this.tt = e({
                XMLHttpRequest: !0,
                eventTarget: !0,
                requestAnimationFrame: !0,
                setInterval: !0,
                setTimeout: !0
            }, n)
        }
        return t.prototype.setupOnce = function() {
            this.tt.setTimeout && C(xn, "setTimeout", _r),
            this.tt.setInterval && C(xn, "setInterval", _r),
            this.tt.requestAnimationFrame && C(xn, "requestAnimationFrame", jr),
            this.tt.XMLHttpRequest && "XMLHttpRequest"in xn && C(XMLHttpRequest.prototype, "send", kr);
            var t = this.tt.eventTarget;
            t && (Array.isArray(t) ? t : wr).forEach(Sr)
        }
        ,
        t.id = "TryCatch",
        t
    }();
    function _r(t) {
        return function() {
            for (var n = [], r = 0; r < arguments.length; r++)
                n[r] = arguments[r];
            var e = n[0];
            return n[0] = Dn(e, {
                mechanism: {
                    data: {
                        function: V(t)
                    },
                    handled: !0,
                    type: "instrument"
                }
            }),
            t.apply(this, n)
        }
    }
    function jr(t) {
        return function(n) {
            return t.apply(this, [Dn(n, {
                mechanism: {
                    data: {
                        function: "requestAnimationFrame",
                        handler: V(t)
                    },
                    handled: !0,
                    type: "instrument"
                }
            })])
        }
    }
    function kr(t) {
        return function() {
            for (var n = [], r = 0; r < arguments.length; r++)
                n[r] = arguments[r];
            var e = this
              , i = ["onload", "onerror", "onprogress", "onreadystatechange"];
            return i.forEach((function(t) {
                t in e && "function" == typeof e[t] && C(e, t, (function(n) {
                    var r = {
                        mechanism: {
                            data: {
                                function: t,
                                handler: V(n)
                            },
                            handled: !0,
                            type: "instrument"
                        }
                    }
                      , e = H(n);
                    return e && (r.mechanism.data.handler = V(e)),
                    Dn(n, r)
                }
                ))
            }
            )),
            t.apply(this, n)
        }
    }
    function Sr(t) {
        var n = xn
          , r = n[t] && n[t].prototype;
        r && r.hasOwnProperty && r.hasOwnProperty("addEventListener") && (C(r, "addEventListener", (function(n) {
            return function(r, e, i) {
                try {
                    "function" == typeof e.handleEvent && (e.handleEvent = Dn(e.handleEvent, {
                        mechanism: {
                            data: {
                                function: "handleEvent",
                                handler: V(e),
                                target: t
                            },
                            handled: !0,
                            type: "instrument"
                        }
                    }))
                } catch (t) {}
                return n.apply(this, [r, Dn(e, {
                    mechanism: {
                        data: {
                            function: "addEventListener",
                            handler: V(e),
                            target: t
                        },
                        handled: !0,
                        type: "instrument"
                    }
                }), i])
            }
        }
        )),
        C(r, "removeEventListener", (function(t) {
            return function(n, r, e) {
                var i = r;
                try {
                    var o = i && i.__sentry_wrapped__;
                    o && t.call(this, n, o, e)
                } catch (t) {}
                return t.call(this, n, i, e)
            }
        }
        )))
    }
    var xr = function() {
        function t(n) {
            void 0 === n && (n = {}),
            this.name = t.id,
            this.dt = n.key || "cause",
            this.yt = n.limit || 5
        }
        return t.prototype.setupOnce = function() {
            var n = nn().getClient();
            n && Yt((function(r, e) {
                var i = nn().getIntegration(t);
                return i ? function(t, n, r, e, i) {
                    if (!(e.exception && e.exception.values && i && m(i.originalException, Error)))
                        return e;
                    var o = Or(t, r, i.originalException, n);
                    return e.exception.values = u(o, e.exception.values),
                    e
                }(n.getOptions().stackParser, i.dt, i.yt, r, e) : r
            }
            ))
        }
        ,
        t.id = "LinkedErrors",
        t
    }();
    function Or(t, n, r, e, i) {
        if (void 0 === i && (i = []),
        !m(r[e], Error) || i.length + 1 >= n)
            return i;
        var o = Nn(t, r[e]);
        return Or(t, n, r[e], e, u([o], i))
    }
    var Rr = function() {
        function t() {
            this.name = t.id
        }
        return t.prototype.setupOnce = function() {
            Yt((function(n) {
                if (nn().getIntegration(t)) {
                    if (!xn.navigator && !xn.location && !xn.document)
                        return n;
                    var r = n.request && n.request.url || xn.location && xn.location.href
                      , i = (xn.document || {}).referrer
                      , o = (xn.navigator || {}).userAgent
                      , u = e(e(e({}, n.request && n.request.headers), i && {
                        Referer: i
                    }), o && {
                        "User-Agent": o
                    })
                      , a = e(e(e({}, n.request), r && {
                        url: r
                    }), {
                        headers: u
                    });
                    return e(e({}, n), {
                        request: a
                    })
                }
                return n
            }
            ))
        }
        ,
        t.id = "HttpContext",
        t
    }()
      , Tr = function() {
        function t() {
            this.name = t.id
        }
        return t.prototype.setupOnce = function(n, r) {
            var e = function(n) {
                if (n.type)
                    return n;
                var e = r().getIntegration(t);
                if (e) {
                    try {
                        if (function(t, n) {
                            if (!n)
                                return !1;
                            if (function(t, n) {
                                var r = t.message
                                  , e = n.message;
                                if (!r && !e)
                                    return !1;
                                if (r && !e || !r && e)
                                    return !1;
                                if (r !== e)
                                    return !1;
                                if (!Nr(t, n))
                                    return !1;
                                if (!Dr(t, n))
                                    return !1;
                                return !0
                            }(t, n))
                                return !0;
                            if (function(t, n) {
                                var r = Ar(n)
                                  , e = Ar(t);
                                if (!r || !e)
                                    return !1;
                                if (r.type !== e.type || r.value !== e.value)
                                    return !1;
                                if (!Nr(t, n))
                                    return !1;
                                if (!Dr(t, n))
                                    return !1;
                                return !0
                            }(t, n))
                                return !0;
                            return !1
                        }(n, e.bt))
                            return null
                    } catch (t) {
                        return e.bt = n
                    }
                    return e.bt = n
                }
                return n
            };
            e.id = this.name,
            n(e)
        }
        ,
        t.id = "Dedupe",
        t
    }();
    function Dr(t, n) {
        var r = Ir(t)
          , e = Ir(n);
        if (!r && !e)
            return !0;
        if (r && !e || !r && e)
            return !1;
        if (r = r,
        (e = e).length !== r.length)
            return !1;
        for (var i = 0; i < e.length; i++) {
            var o = e[i]
              , u = r[i];
            if (o.filename !== u.filename || o.lineno !== u.lineno || o.colno !== u.colno || o.function !== u.function)
                return !1
        }
        return !0
    }
    function Nr(t, n) {
        var r = t.fingerprint
          , e = n.fingerprint;
        if (!r && !e)
            return !0;
        if (r && !e || !r && e)
            return !1;
        r = r,
        e = e;
        try {
            return !(r.join("") !== e.join(""))
        } catch (t) {
            return !1
        }
    }
    function Ar(t) {
        return t.exception && t.exception.values && t.exception.values[0]
    }
    function Ir(t) {
        var n = t.exception;
        if (n)
            try {
                return n.values[0].stacktrace.frames
            } catch (t) {
                return
            }
    }
    var Mr = Object.freeze({
        __proto__: null,
        GlobalHandlers: dr,
        TryCatch: Er,
        Breadcrumbs: $n,
        LinkedErrors: xr,
        HttpContext: Rr,
        Dedupe: Tr
    })
      , Lr = [new jn, new En, new Er, new $n, new dr, new xr, new Tr, new Rr];
    function Cr(t) {
        t.startSession({
            ignoreDuration: !0
        }),
        t.captureSession()
    }
    var qr = {};
    xn.Sentry && xn.Sentry.Integrations && (qr = xn.Sentry.Integrations);
    var Ur = e(e(e({}, qr), Sn), Mr);
    return t.Breadcrumbs = $n,
    t.BrowserClient = zn,
    t.Dedupe = Tr,
    t.FunctionToString = En,
    t.GlobalHandlers = dr,
    t.HttpContext = Rr,
    t.Hub = Qt,
    t.InboundFilters = jn,
    t.Integrations = Ur,
    t.LinkedErrors = xr,
    t.SDK_VERSION = wn,
    t.Scope = Kt,
    t.TryCatch = Er,
    t.WINDOW = xn,
    t.addBreadcrumb = function(t) {
        nn().addBreadcrumb(t)
    }
    ,
    t.addGlobalEventProcessor = Yt,
    t.captureEvent = function(t, n) {
        return nn().captureEvent(t, n)
    }
    ,
    t.captureException = captureException,
    t.captureMessage = function(t, n) {
        var r = "string" == typeof n ? n : void 0
          , e = "string" != typeof n ? {
            captureContext: n
        } : void 0;
        return nn().captureMessage(t, r, e)
    }
    ,
    t.chromeStackLineParser = nr,
    t.close = function(t) {
        var n = nn().getClient();
        return n ? n.close(t) : St(!1)
    }
    ,
    t.configureScope = function(t) {
        nn().configureScope(t)
    }
    ,
    t.createTransport = mn,
    t.defaultIntegrations = Lr,
    t.defaultStackLineParsers = vr,
    t.defaultStackParser = hr,
    t.eventFromException = Cn,
    t.eventFromMessage = qn,
    t.flush = function(t) {
        var n = nn().getClient();
        return n ? n.flush(t) : St(!1)
    }
    ,
    t.forceLoad = function() {}
    ,
    t.geckoStackLineParser = ir,
    t.getCurrentHub = nn,
    t.getHubFromCarrier = rn,
    t.init = function(t) {
        void 0 === t && (t = {}),
        void 0 === t.defaultIntegrations && (t.defaultIntegrations = Lr),
        void 0 === t.release && ("string" == typeof __SENTRY_RELEASE__ && (t.release = __SENTRY_RELEASE__),
        xn.SENTRY_RELEASE && xn.SENTRY_RELEASE.id && (t.release = xn.SENTRY_RELEASE.id)),
        void 0 === t.autoSessionTracking && (t.autoSessionTracking = !0),
        void 0 === t.sendClientReports && (t.sendClientReports = !0);
        var n, r = e(e({}, t), {
            stackParser: (n = t.stackParser || hr,
            Array.isArray(n) ? z.apply(void 0, u(n)) : n),
            integrations: vn(t),
            transport: t.transport || (Q() ? Kn : Vn)
        });
        !function(t, n) {
            !0 === n.debug && console.warn("[Sentry] Cannot initialize SDK with `debug` option using a non-debug bundle.");
            var r = nn()
              , e = r.getScope();
            e && e.update(n.initialScope);
            var i = new t(n);
            r.bindClient(i)
        }(zn, r),
        t.autoSessionTracking && function() {
            if (void 0 === xn.document)
                return;
            var t = nn();
            if (!t.captureSession)
                return;
            Cr(t),
            ot("history", (function(t) {
                var n = t.from
                  , r = t.to;
                void 0 !== n && n !== r && Cr(nn())
            }
            ))
        }()
    }
    ,
    t.lastEventId = function() {
        return nn().lastEventId()
    }
    ,
    t.makeFetchTransport = Kn,
    t.makeMain = tn,
    t.makeXHRTransport = Vn,
    t.onLoad = function(t) {
        t()
    }
    ,
    t.opera10StackLineParser = fr,
    t.opera11StackLineParser = sr,
    t.setContext = function(t, n) {
        nn().setContext(t, n)
    }
    ,
    t.setExtra = function(t, n) {
        nn().setExtra(t, n)
    }
    ,
    t.setExtras = function(t) {
        nn().setExtras(t)
    }
    ,
    t.setTag = function(t, n) {
        nn().setTag(t, n)
    }
    ,
    t.setTags = function(t) {
        nn().setTags(t)
    }
    ,
    t.setUser = function(t) {
        nn().setUser(t)
    }
    ,
    t.showReportDialog = function(t, n) {
        if (void 0 === t && (t = {}),
        void 0 === n && (n = nn()),
        xn.document) {
            var r = n.getStackTop()
              , i = r.client
              , o = r.scope
              , u = t.dsn || i && i.getDsn();
            if (u) {
                o && (t.user = e(e({}, o.getUser()), t.user)),
                t.eventId || (t.eventId = n.lastEventId());
                var a = xn.document.createElement("script");
                a.async = !0,
                a.src = function(t, n) {
                    var r = T(t)
                      , e = un(r) + "embed/error-page/"
                      , i = "dsn=" + O(r);
                    for (var o in n)
                        if ("dsn" !== o)
                            if ("user" === o) {
                                var u = n.user;
                                if (!u)
                                    continue;
                                u.name && (i += "&name=" + encodeURIComponent(u.name)),
                                u.email && (i += "&email=" + encodeURIComponent(u.email))
                            } else
                                i += "&" + encodeURIComponent(o) + "=" + encodeURIComponent(n[o]);
                    return e + "?" + i
                }(u, t),
                t.onLoad && (a.onload = t.onLoad);
                var f = xn.document.head || xn.document.body;
                f && f.appendChild(a)
            }
        }
    }
    ,
    t.startTransaction = function(t, n) {
        return nn().startTransaction(e({}, t), n)
    }
    ,
    t.winjsStackLineParser = ur,
    t.withScope = on,
    t.wrap = function(t) {
        return Dn(t)()
    }
    ,
    t
}({});
//# sourceMappingURL=bundle.es5.min.js.map
