# Zabbix-Items-LinkedIn-Folowers
A common way to get information about social media profiles is to use the API. However, this usually requires sifting through a more or less complicated process of obtaining an API Token.

Here's a demonstration of how to do it differently.

## The first thing we will need is a LinkedIn company ID. 

One option is to follow the official official LinkedIn documentation:

> As a company page administrator, your Company ID can be retrieved by navigating to the admin section of your company page. For example, the LinkedIn Company Admin Page is 
> https://www.linkedin.com/company/0000/admin/. We will use the Company ID 0000 in our example.

In our case we get company ID: 76503092

![Image of companyId](images/companyid.png "Company ID")

## The next step in this demonstration is to create a basic guest to monitor the number of followers.

**Host**: Followers

**Host groups**: Followers

![Image of host creation](images/host.png "Image of host creation")

## And now let's create the item itself.

**Name:** LinkedIn: InitMAX page followers count

**Key:** linkedin.follower.count.initmax
**Parameters:** 
|  Name       | Value       |
| ----------- | ----------- |
| companyId   | 76503092    | 

**Script:** 
```javascript
params = JSON.parse(value)

var request = new HttpRequest();
return request.get("https://www.linkedin.com/pages-extensions/FollowCompany?id=" + params.companyId + "&counter=bottom");
```

**Update interval:** 15m

![Image of item creation](images/item.png "Image of item creation")

### In this case, we must also create preprocessing.

|  Name       | Parameters              |
| ----------- | ----------- | ----------- |
| Regular expression: | follower-count">(\S+)< | \1
| Replace: | , | leave blank

![Image of prepsocessing creation](images/preprocessing.png "Image of prepsocessing creation")


## And we're almost done, now let's test the item.

Go back to záložku item clik **Test** button and then klick on **Get value and test** and ..... BANANA 🍌 🙂 (thanks [Steve DESTIVELLE](https://www.linkedin.com/in/steve-destivelle-88b6b389/) )

![Image of item testing](images/test.png "Image of item testing")


## Now save the item and you are done. 
Enjoy the growing numbers of folowers on LinkedIn profile without API.  🙂