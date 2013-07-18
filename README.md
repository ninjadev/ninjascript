# Ninjascript

<table>
<tr>
<th>Ninjascript</th>
<th>Compiled JS output</th>
</tr>
<tr>
<td>
<pre><code>
/* src/namespace/SomeObject */

someMemberVariable = "hello world"

SOME_STATIC_CONSTANT = "some value"

someMethod(a, b, c){
    scopedVariable = "someMethod was called"
    log(scopedVariable, a, b, c) 
}

someMethodThatReturnsSomething(a, b){
    &lt; a * b
}

someStaticMethod(a, b){{
    log("this is what a static method looks like", a, b)
}}

someAnonymousFunction = (a, b, c, d){
    log(a, b, c, d)
}

(a, b){
    log("self-invoked function expression", a, b)
}(1, 2)
</code></pre>
</td>
<td>
<pre><code>
/* gen/namespace/SomeObject.js */
namespace.SomeObject = function(){
    "use strict";

    function SomeObject(){
        this.someMemberVariable = "hello world";
    }

    SomeObject.SOME_STATIC_CONSTANT = "some value";

    SomeObject.prototype.someMethod = function(a, b, c){
        var scopedVariable = "someMethod was called";
        console.log(scopedVariable, a, b, c);
        return this;
    }

    SomeObject.prototype.someMethodThatReturnsSomething = function(a, b){
        return a * b;
    }

    SomeObject.someStaticMethod = function(a, b){
        console.log("this is what a static method looks like", a, b)
        return SomeObject;
    }

    SomeObject.prototype.someAnonymousFunction = function(a, b, c, d){
        console.log(a, b, c, d);
        return this;
    }

    (function(a, b){
        console.log("self-invoked function expression", a, b);
        return this;
    })(1, 2);

    return SomeObject;
}
</code></pre>
</td>
</tr>
</table>
