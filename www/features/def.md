
## The `def` Feature

### Syntax

```ebnf
def <function name>(<parameter list>)
  {<command>} 
[catch <identifier>
  {<command>}]
end
```

The `def` keyword allows you to define functions in hyperscript.  It consists of a function name, a paramter list
and a body, with an optional catch block.

The body of the function is a list of [commands](/docs#commands), optionally separated by the `then` keyword.

Functions are typically placed in script tags:

```html
<script type="text/hyperscript">
  def delayTheAnswer()
    wait 2s
    return 42
  end
</script>
```

You may also namespace functions by giving them a dot separated namespace

```html
<script type="text/hyperscript">
  def utils.delayTheAnswer()
    wait 2s
    return 42
  end
</script>
```

Functions may be invoked from both hyperscript or javascript.  However, in javascript, an asynchronous function will
return a promise that must be dealt with explicitly.

### <a name="return"></a>[Return](#return)

Values may be returned with the `return` command.  If the function is synchronous, the value will be returned as normal
and if it is asynchronous, the promise will be resolved.  The hyperscript runtime hides this difference when the
function is invoked within hyperscript.

### <a name="throw"></a>[Throw](#throw)

Exceptions may be thrown with the `throw` command.  If the function is synchronous, the exception will be thrown as normal
and if it is asynchronous, the promise will be rejected.  The hyperscript runtime hides this difference when the
function is invoked within hyperscript.

### <a name="exceptions"></a>[Exceptions](#exceptions)

Hyperscript functions support a single catch block that can be used to catch exceptions that are throw synchronously
or asynchronously

```html
<script type="text/hyperscript">
  def delayTheAnswer()
    wait 2s
    throw "Nope!"
  catch e
    return e
  end
</script>

```
