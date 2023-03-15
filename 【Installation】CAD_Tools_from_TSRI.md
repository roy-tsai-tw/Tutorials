# CAD Tool Installation Problems & Solutions
* Please follow the steps from TSRI to install those EDA tools. I only list some problems and solutions I've faced before.


## EDA Tools: Command Not Found 
### Incisive

### JasperGold

### Formal LEC
* Solution: Change the following command in forml.cshrc file:
```
set bin_prefix 	= "tools/bin"

           to
              
              
set bin_prefix 	= "bin"
```

