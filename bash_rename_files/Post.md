Smartes Renamen:

filenamen sind video_ZAHL - ziehe dekrementiere zahl und speichere wieder neu
```
#!/bin/bash

for file in $(ls old)
do
	num=$(echo  $file | cut -f"1" -d"." | cut -f"2" -d"_")
	
	(( num-- ))
	mv "old/$file" "new/video_$num.avi"
done
```
