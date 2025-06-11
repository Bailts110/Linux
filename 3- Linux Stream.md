[[2-Linux Command]]
[[0-History of Linux]]
In linux There is Data Stream Significant Text Stream and it Divided into 
#Shell #Linux #DataStream_Linux

| type               | defenition                                  |     |
| ------------------ | ------------------------------------------- | --- |
| Standard Stream    | Data That Come in/from Terminal             |     |
| nonStandard Stream | That Service write on File without Terminal |     |
and Standard Stream Divided into 
- Input Stream 
- Output Stream
- Error Stream
>[!note] The Command in Shell Consist of Tokens that Delimiter Between it
>like `ls -l -a` -- `ls`is token , `-l` is Token `-a` is Token and all of It is **Standard Input** and The Delimiter is Space Between Tokens 

--------
#### Redirection Input/Output Stream in linux
>[!note] The Default Pipes like Output is From Shell To Terminal 
But When Can make Redirect Output From Shell To File like
`ls -l ~ > output` in Here he Redirect the Output to File output 
and `>` is Overrinde the Result to Append Result us `>>` like `ls -l >> output`
To Redirect Error Message `2>` => `ls /err 2> ouput` =>

--------------------
### Pipes and Filter 
Means that Before the Command go to Through pipes before reach the final output like Terminal 
like 
`Head -n 5 hosts` in Here it get the Text then make filter on it to get first 5 Sentence :) and there is tail `tail -n 5 hosts` 

`wc` Command Word Count in File `wc hosts` 
`wc -l -w -c hosts`

> [!note] The Best Using of **Pipes** 
> - is `|` between Command as output of Command before it is input to Command After it like 	`head -n 55 /var/log/syslog | grep Inserted` so in this code it get the 55 line of file then pass it as Pipes Stream to Next Command that is Search on Output
> - another Example `int1=$(head -n 55 /var/log/syslog | grep Inserted | wc -l) `

---------------

![[Screenshot from 2025-06-07 21-35-43.png]]
>[!note] example of Pipes using `tr`  
>with options like `-d` to delete ,`[i] [I]` to replace Selected Char with another ,,,`-s` to delete the Repeated char 
> `[:digit:]` represent digit ,,
> `[:lower:] [:upper:]` represent character Case
> 

### Cut
>[!note] Cut Example
>![[Screenshot from 2025-06-07 22-21-01 3.png]]
remove section of text 
`cut -c 1` for for get first char
`cut -b 1` to get first byte
`cut -c 2,20` to get second and 20th chaar 
`cut -f 1` to get first field but it take the whole text if not  Specify Delimeter First so Specify Delimter with `cut -f 1 -d " "`

