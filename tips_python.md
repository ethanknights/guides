## Reimporting modules
### Manually (importlib)
```py
import importlib
importlib.reload(ConnectPython)
```


### Automatically (PyCharm)
Enable auto-reimport after save (pycharm)
https://stackoverflow.com/questions/33323707/how-do-i-reload-a-module-after-changing-it <br>
Ensure ```pip install ipython``` & add the following code to <br>
```Preferences > BuildExecutionDeployment > Console > PythonConsole > StartingScript```:
```py
%load_ext autoreload
%autoreload 2
```


## Init pd array
### A) Inherit data from another pd.series:
```py
pd.DataFrame(dat, columns = ["name", "age"])
```

### B) NaN dataframe
```py
df = pd.DataFrame(index=range(nExpectedVisits),columns=range(2))
```

### C) Flexibly init a specific datatype, per column
```py
    df = pd.DataFrame({'visitTypeKey': [99999]          * nExpectedVisits,
                       'expected_date': ['01/01/9999']  * nExpectedVisits,  
                       'expected_time': ['00:00:00']    * nExpectedVisits,  
                       'name':          ['NaN']         * nExpectedVisits,
                       'checkin':       ['NaN']         * nExpectedVisits,
                       'studyDays':     ['NaN']         * nExpectedVisits,
                       })
```


## Loop through pd and set values at index:

```py
for i in range(0,len(df_expectedVisitDatetime)):
    if df_expectedVisitDatetime.iloc[i].get('check_visitOnThisDate') == True:
        df_expectedVisitDatetime['compliance'].iloc[i] = 'completed'
```


## List Column Headers
```py
df.columns.tolist()
```


## List unique row values
```py
df_audit['Field'].unique().tolist
```


## Index a dataframe
```py
QC_case = QC_cases.iloc[0]
QC_case = QC_cases.iloc['Date of Birth'][0]
```


## Trim string (A. by index; B. str repalce)
```py
df_RPS = df_RPS['Visit Start (GMT)'].str[:-4]
df_RPS = df_RPS['Visit Start (GMT)'].str.replace(r' UTC','')
```


## find(idx)
```py
np.where(idx)
```


## find pd idx
```py
tmpCheck = pd.Series([True, False, True, True, False, False, False, True])
tmpCheck[tmpCheck].index
```


## Date time stuff
```py
toCheck_visitStart = datetime.strptime(toCheck_visitStart, '%Y.%m.%d %H:%M:%S') + timedelta(0,1) #i.e. Visit Start + 1 sec
toCheck_visitStart = str(toCheck_visitStart.strftime('%Y.%m.%d %H:%M:%S'))
```

```py
tmpDate = date(int(toCheck_newVal[0:4]), int(toCheck_newVal[6]), int(toCheck_newVal[8]))
tmpDate.strftime('%YYYY/%MM/%DD')
```

```py
def convertAuditValues_DOB(toCheck_newVal):
    # Convert DOB to same format str (pd not auto-detecting datetime so end with strings ...)
    toCheck_newVal = toCheck_newVal[8:10] + '/' + toCheck_newVal[5:7] + '/' + toCheck_newVal[0:4]
    toCheck_newVal = datetime.strptime(toCheck_newVal,'%d/%m/%Y')
    toCheck_newVal = str(toCheck_newVal.strftime('%d/%b/%Y'))
    return toCheck_newVal
```


## Write df to csv
```py
df.to_csv(path_or_buf='tmp.csv')
```


## Add rowNumber column to a dataframe
```py
df_audit['Row_Number'] = np.arange(len(df_audit))
```


## Join a list of strings with a separator
```py
list_measures = ['DEANY',
'DEBAD',
'DEDIZZ']
str_measures = '|'.join(list_measures)
```


## Define a function
```py
def gatherQCfields(QC_case):
    toCheck_subjID = QC_case['ID1']
    toCheck_visitStart = QC_case['Visit Start']
    return toCheck_subjID, toCheck_visitStart
```


## fprintf
```py
print(f'Written log of cases that failed QC to:\n{logName}')
```


## Print an entire df row (no truncate)
```py
print(df.iloc[977].to_string())
```


## List dict keys
```py
print(studyInfo.keys())
dict_keys(['appId', 'studyDaySetup'])
```


## Use .remove
```py
import numpy as np

num_list = [1,2,3,4,5]
num_list.remove(2)
print(num_list)
```


## Delimit-split a string 
```py
y = 'stuff;thing;junk'
z = y.split(';')
len(z)
```


## Using includes in an API call
```py
GUIDs['siteName'] = '5008'  # '2120'       # studySites = ConnectPython.getStudySites(config, GUIDs.get('studyID')); tmp = json.dumps(studySites, sort_keys = True, indent = 4); print(tmp)
includes = ['id', 'address', 'name', 'siteId']
site = ConnectPython.getStudySite(config, GUIDs.get('studyID'), GUIDs.get('siteName'))

# Get List of Subjects
# ============================
includes = ['subjectIds']
subjects = ConnectPython.getSubjectIDs(config, site.get('id'), includes) 
```


## Naturally sort (numerically) a glob-list

```py
from natsort import natsorted


dirPath = 'data/bodies'

read_images(dirPath)
def read_images(dirPath)

    print(natsorted(glob.glob(os.path.join(dirPath, '*.bmp'))))
    return
```

