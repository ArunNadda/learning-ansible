## 04 - yaml

### ansible is python base, lets check how python reads yml files
### we will practice writing yml and test syntax with python

#### rev 01
##### blank yml file

#### rev 02
##### key:value, value is string (no requirement to quote)


#### rev 03
##### key:value, value is string (with quotes)

#### rev 04
##### key:value, value is string
##### shows difference between quotes

#### rev 05
##### line folding using pipe (|)
##### it includes \n (new line)


#### rev 06
##### line folding using pipe (>)


#### rev 07
##### line folding using pipe (>-)


#### rev 08
##### int

```
>>> import yaml
>>> yaml.load(open("test.yml"))
{'int1': 1}
>>> myvar=yaml.load(open("test.yml"))
>>> print(myvar['int1'])
1
>>> print(type(myvar['int1']))
<type 'int'>
>>>
>>>
```


#### rev09
##### number as string
```
>>> import yaml
>>> yaml.load(open("test.yml"))
{'int1': '1'}
>>> myvar=yaml.load(open("test.yml"))
>>> print(myvar['int1'])
1
>>> print(type(myvar['int1']))
<type 'str'>
>>>
```



#### rev10
##### true and false


#### rev11
##### list/array


#### rev12
##### dict (same as rev01)


#### rev13
##### dict (written in python way)



#### rev14
##### list (written in python way)



#### rev15
##### incorrect yml syntax (both list and dict cannot be at same indentation)

#### rev16
##### incorrect yml syntax (both list and dict cannot be at same indentation)
##### same behaviour in python way




#### rev17
##### lists nested in dict


#### rev18
##### lists nested in dict of lists

#### rev19
##### more nesting

#### rev20
##### practice

```
create lists of 4 car brand
1. Aston Martin
2. Fiat
3. Ford
4. Vauxhall
```

#### rev21
##### practice

```
add year founded and website to each car brand

Aston Martin, year_founded is 1913, website is astonmartin.com
Fiat, year_founded is 1899, website is fiat.com
Ford, year_founded is 1903, website is ford.com
Vauxhall, year_founded is 1857, website is vauxhall.co.uk
```

#### rev22
##### practice


```
add founder under each brand

Aston Martin, Lionel Martin and Robert Bamford (in a list)
Fiat, Giovanni Agnelli
Ford, Henry Ford
Vauxhall, Alexander Wilson

```


