# Accessing Web APIs from R

Resources for accessing web APIs from R.

[Using Web APIs from R](https://www.rstudio.com/resources/videos/using-web-apis-from-r/)

[Configuring R to Use an HTTP or HTTPS Proxy](https://support.rstudio.com/hc/en-us/articles/200488488-Configuring-R-to-Use-an-HTTP-or-HTTPS-Proxy)

[What is an API?](https://www.youtube.com/watch?v=s7wmiS2mSXY)

[HTTP: The Protocol Every Web Developer Must Know](https://code.tutsplus.com/tutorials/http-the-protocol-every-web-developer-must-know-part-1--net-31177)

## Quick Start guide

This informal guide is written from experience using the [Care Opinion API](https://www.careopinion.org.uk/info/api-v2) while working for NHS National Services Scotland ([repo if you're curious](https://github.com/jsphdms/care-opinion-api)). Most of the steps are generic however some details may differ (e.g. domain names and operating systems).

### Step 1
Find your .Renviron file. If you're on Windows this is usually in your Documents folder.

### Step 2
Open your .Renviron file with a text editor and add this line:

`https_proxy = proxy.your.domain.name:port`

Where **your.domain.name** is the domain of the organisation you're sending requests from and **port** is a 4 digit port number. You should be able to get both these from your IT department.

### Step 3
Follow the examples in [this httr guide](https://cran.r-project.org/web/packages/httr/vignettes/quickstart.html).

### Step 4a - Get a key
Some APIs require authentication. This may simply involve emailing whoever looks after the API and requesting a key (usually a jumbled string of letters and numbers). Or it may mean subscribing to the API as a paid service. Your organisation may already subscribe without you knowing so it's best to check with whoever knows these things.

If you have a key save it in your .Renviron file like this:

`co_api_key = lotsofrandomlettersandnumbers`

Then load it into your R session like this:

`api_key <- Sys.getenv("co_api_key")`

You can now use the variable `api_key` in your script like any other variable. This is more secure than saving your key directly in your script because you might forget it's there and accidentally share your script with someone who shouldn't see it.

### Step 4b - Research the API
Each API is different. It's tempting to jump straight into submitting GET requests. But researching the API properly will save a **lot** of time in the long run. Look for documentation. Specifically look out for: **endpoints**, **enumeration**, and **filtering**. 

Here's an example of a documented API: https://www.careopinion.org.uk/info/api-v2

Some APIs aren't documented. These are best avoided unless you are comfortable with APIs. That said - using undocumented APIs isn't unheard of. [Here's an example](http://enpiar.com/2017/08/11/one-hour-package/) of someone wrapping an undocumented API with an R package.

### Step 4c - Start small
First focus on submitting a minimal GET request that results in a 200 (successful) status code in your response.

### Step 4d - Build gradually
Once you have a 200 status code gradually build up the complexity until you have what you need. Check if you're getting real data as you go. Don't infer success from the absence of an error message.

### Step 4e - Tidy and analyse
Congratulations! You have completed the **import** part of this process:

![A model of the tools needed in a typical data science project](http://r4ds.had.co.nz/diagrams/data-science.png)

The next step is **tidying**. Web APIs usually return XML or JSON so try [xml2](https://github.com/r-lib/xml2) or [jsonlite](https://www.opencpu.org/posts/jsonlite-a-smarter-json-encoder/) to get your data into an R object like a dataframe.
