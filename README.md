# Settings for Python

Simplistic class for class related settings inside Python

## Documentation

#### self.get_setting(key, default)

> **key**: The nested key as a string, dot seperated. Example: `foo.bar.foo`  
> **default**: If the given key does not exist, or returns an error, the default value is returned. Default: `None`

That's it.

## How to use

### Project specific settings

You can create a project specific settings class by creating a file that extends from `pysettings.Settings`.

```python
# default.py
    
from pysettings import Settings
    
class DefaultSettings(Settings):
    
    def __init__(self):
        super().__init__()
        
        self.settings = {
            'foo': {
                'bar': 1
            }
        }
```

Using this class in your master class to inherit every functionality from the py-settings module.

```python
# dummy.py
    
from default import DefaultSettings
    
class Dummy(DefaultSettings):
    
    def __init__(self):
        super().__init__()
        
    def run(self):
        is_enabled = self.get_setting('foo.bar', 0)
        
        print(is_enabled) # returns 1
```

### Class specific settings

You can also create class specific settings by overriding the defaults inside the class.

```python
# dummy.py
    
from pysettings import Settings

class Dummy(Settings):
    
    def __init__(self):
        super().__init__()
        
        self.settings = {
            'bar' : 'foo'
        }
        
    def run(self):
        is_enabled = self.get_setting('foo.bar', 0)
        
        print(is_enabled) # returns 0
        
        is_foo = self.get_setting('bar', 'bar')
        
        print(is_foo) # returns 'foo'
```

## Future ideas

- Method to override certain options instead of all options inside a class
- ?