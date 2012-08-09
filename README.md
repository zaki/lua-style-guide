# Document format

* Use UTF-8
* Use LF line endings
* Use 2 spaces for indentation
* Don't use tabs
* Don't leave trailing spaces

# Naming

* constants use ```UPCASE_SNAKE```
* variable names use ```lower_case_snake```
* class-like structures use ```CamelCase```
* other functions use ```smallCamelCase```
* Use ```_``` for unneeded variables
* Don't use Hungarian Notation

    ```Lua
    local DISTANCE_MAXIMUM   = 1
    local distance_to_target = 0
    local function distanceToTarget() end
    local function TargetFactory() end

    for _,v in ipairs(table) do
      print(v)
    end
    ```

# Layout

* Use spaces around operators

    ```Lua
    -- bad
    local a=1*2
    local s='a'..'b'

    -- good
    local a = 1 * 2
    local s = 'a' .. 'b'
    ```

* No spaces after ```( [``` and before ```] )```

    ```Lua
    -- bad
    function badFunction( argument1, argument2 )
    end
    badFunctionCall( )

    -- good
    function goodFunction(argument1, argument2)
    end
    goodFunctionCall()
    ```

* Align assignments, function arguments etc. with spaces

    ```Lua
    -- bad
    local a = 1
    local long_identifier = 2

    -- good
    local a               = 1
    local long_identifier = 2

    -- bad
    sysCommand(form, UI_FORM_UPDATE_NODE, 'a', FORM_NODE_VISIBLE, false)
    sysCommand(form, UI_FORM_UPDATE_NODE, 'sample', FORM_NODE_VISIBLE, false)

    -- good
    sysCommand(form, UI_FORM_UPDATE_NODE, 'a',      FORM_NODE_VISIBLE, false)
    sysCommand(form, UI_FORM_UPDATE_NODE, 'sample', FORM_NODE_VISIBLE, false)
    ```

* Leave an empty line between function definitions

    ```Lua
    -- bad
    function a()
    end
    function b()
    end

    -- good
    function a()
    end

    function b()
    end
    ```

# Comments

* Don't write unnecessary comments. Make code simpler so that comments are not necessary
* If comments are necessary, use single line comments (--)
* Use a single space between the comment mark and the text (eg ```-- text```)
* It's OK to document functions, but avoid documenting locals
* Use luadoc docstrings for documenting comments

    ```Lua
    --bad comment
    -- good comment

    -- This is probably unnecessary
    -- @param: arg Argument
    local function good(arg)
    end

    -- This is OK
    -- @param: arg Argument
    function good(arg)
    end
    ```

* Use ```@param``` and ```@return``` when needed
* Avoid ```@author```, ```@copyright```
* Don't leave commented out code in. Use the version control system as backup

# Annotations

* Use TODO: and FIXME: tags
* Optionally add person responsible to the end of the comment in parenthesis (normally use bug tracking system or even `git[-svn] blame`)

* TODO indicates a missing feature to be implemented later
* FIXME indicates a problem in the existing code (inefficient implementation, bug, unnecessary code, etc)
* Avoid using other tags unless really necessary

    ```Lua
    -- TODO: implement method (Zaki)
    function a()
      -- FIXME: check conditions
    end
    ```

# Scopes

* Prefer to use locals whenever possible
* Prefer to use modules instead of polluting the global scope
* Prefer to create local aliases when requiring a module

# Strings

* Prefer double-quoted strings

    ```Lua
    -- ok
    local string = 'string'

    -- better
    local string = "string"
    ```

# Functions

* Keep functions short (15-20 lines). Separate longer functions into smaller sub-functions
* Keep argument list shorter than 3 or 4 parameters
* Avoid one-lining functions

    ```Lua
    -- bad
    function bad() return 0 end
    function longArgumentList(arg1, arg2, arg3, arg4, arg5, arg6)
    end

    -- good
    function good()
      return 0
    end

    function optionTable(options)
    end
    ```

* Functions should have a single place of return. It is OK to early-return

    ```Lua
    -- bad
    function badFunction(arg)
      if arg == 1 then
        -- process for 1
        return 0
      elseif arg == 2 then
        -- process for 2
        return 5
      elseif arg == 3 then
        -- process for 3
        return -2
      else
        -- process for others
        return 7
      end

    end

    -- good
    function goodFunction(arg)
      if not arg then return 0 end

      -- process

      return 1
    end
    ```

* Indent argument list to align to first argument when inserting line-break

    ```Lua
    -- bad
    badCall(arg1,
    arg2,
    arg3,
    arg4
    )

    -- good
    goodCall(arg1,
             arg2,
             arg3,
             arg4)
    ```

* Prefer colon-syntax to explicit self argument

    ```Lua
    -- bad
    function Class.method(self, arg1, arg2)
    end

    -- good
    function Class:method(arg1, arg2)
    end
    ```

# Tables

* Break longer assignment to multiple lines
* Align keys when broken over multiple lines
* Use comma as separator
* Prefer to use comma after the last item

    ```Lua
    -- bad
    table = {key1=val1, key2=val2, key3=val3, key4=val4}

    -- good
    table = {
      key1 = val1,
      key2 = val2,
      key3 = val3,
      key4 = val4,
    }
    ```

# Miscellaneous

* When checking for nil, prefer to use only the variable name

    ```Lua
    -- ok
    if var ~= nil then
    end
    if var == nil then
    end

    -- good
    if var then
    end
    if not var then
    end
    ```

* Prefer single conditional assignment to if-then-else

    ```Lua
    -- bad
    if not x then
      x = 1
    end

    -- good
    x = x or 1
    ```

* Avoid more than 3 levels of nesting
* Use your own judgement to break any of the above rules
