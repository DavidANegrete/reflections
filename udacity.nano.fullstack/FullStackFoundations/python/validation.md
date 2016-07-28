It is encouraged to validate all data that ther server accepts a dictionary is used to validate the months

For example,

```
months = ['January', 'February', 'March', 'April', 'May', 'June',
'July', 'August', 'September', 'October', 'November', 'December']
```

	
```
//Use a dictionary to validate the first three chars
month_abbvs = dict((m[:3].lower(), m) for m in months)
def valid_month(month):
	if month:
		short_month = month[:3].lower()
   		return month_abbvs.get(short_month)
```

```
// Here you have a date validation example
def valid_day(day):
	if day and day.isdigit():
		day = int(day)
		if day > 0 and day <= 31:
			return day
```

```
// Year validation
def valid_year(year):
	if year and year.isdigit():
		year = int(year)
		if year > 1900 and year < 2020:
			return year
```
