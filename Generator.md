### 串接不同的操作 ###
```
def read_line(filename):
    return (line.decode('utf8').rstrip('\n') for line in open(filename))

def filter_comment(lines):
    return (line for line in lines if not line.startswith('#'))

def filter_empty(lines):
    return (line for line in lines if line)

def some_process(filename):
    for line in filter_empty(read_line(filename)):
        ...

def another_process(filename):
    for line in filter_comment(filter_empty(read_line(filename))):
        ...
```
### 將多層迴圈縮成一層迴圈 ###
```
def read_files(filenames):
    for name in filenames:
        for line in open(name):
            yield line.decode('utf8').rstrip('\n')

def grep(pattern, filenames):
    for line in read_files(filenames):
        if re.match(pattern, line):
            print line

def cat(filenames):
    for line in read_files(filenames):
        print line
```

若需要走訪整個目錄下所有檔案，可以使用 os.walk。