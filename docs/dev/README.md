# Development Notes, Diary & Latest Roadmap

Database schema design - text format. Using this [schema design web app](https://app.quickdatabasediagrams.com/#/d/oo35Ob).

```
CustomUser
-
uuid uuid4

# both for web scrapper rating & user input
Company
-
uuid uuid4
user ManyToOne FK >- CustomUser.uuid
labels ManyToMany FK >- Label.uuid
name string
hq_location OneToOne FK >- Address.uuid
home_page OneToOne FK >- Link.uuid
ratings computed
applications computed

CompanyRating
-
uuid uuid4
source OneToOne FK >- Link.uuid
value float
company FK >- Company.uuid


Application
-
uuid uuid4
user ManyToOne FK >- CustomUser.uuid
user_company ManyToOne FK >- Company.uuid
lastest_status computed
statuses computed
position_title string
position_locations computed
job_description_page OneToOne FK >- Link.uuid
labels ManyToMany FK >- Label.uuid
source OneToOne FK >- Link.uuid

PositionLocation
-
uuid
application ManyToOne FK >- Application.uuid
location OneToOne FK >- Address.uuid


Label
-
uuid uuid4
user FK >- CustomUser.uuid
text string
color string
order int

# should we use fixed number? Or user define?
ApplicationStatus
-
uuid uuid4
text string
application ManyToOne FK >- Application.uuid
order int
date date
links computed

Link
-
uuid uuid4
text string
user ManyToOne FK >- CustomUser.uuid
url string
order int

Address
-
uuid uuid4
place_name string
country string
state string
city string
street string
raw_address string
zipcode string

ApplicationStatusLink
-
uuid
link OneToOne FK >- Link.uuid
application_status ManyToOne FK >- ApplicationStatus.uuid
```