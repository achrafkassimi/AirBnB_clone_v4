# 0x06. AirBnB clone - Web dynamic
### `Python` `Front-end` `JavaScript`
## Resources
**Read or watch**:

* [Selector](https://jquery-tutorial.net/selectors/using-elements-ids-and-classes/)
* [Get and set content](https://jquery-tutorial.net/dom-manipulation/getting-and-setting-content/)
* [Manipulate CSS classes](https://jquery-tutorial.net/dom-manipulation/getting-and-setting-css-classes/)
* [Manipulate DOM elements](https://jquery-tutorial.net/dom-manipulation/the-append-and-prepend-methods/)
* [Document ready](https://learn.jquery.com/using-jquery-core/document-ready/)
* [Introduction](https://jquery-tutorial.net/ajax/introduction/)
* [GET & POST request](https://jquery-tutorial.net/ajax/the-get-and-post-methods/)
* [HTTP access control (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

## General
* How cool it is to request your own API
* How to modify an HTML element style
* How to get and update an HTML element content
* How to modify the DOM
* How to make a `GET` request with JQuery Ajax
* How to make a `POST` request with JQuery Ajax
* How to listen/bind to DOM events
* How to listen/bind to user events

## Requirements
### General
* Allowed editors: `vi`, `vim`, `emacs`
* All your files will be interpreted on Chrome (version `57.0`)
* All your files should end with a new line
* A `README.md` file, at the root of the folder of the project, is mandatory
* Your code should be semistandard compliant with the flag `--global $: semistandard *.js --global $`
* All your JavaScript must be in the folder `scripts`
* You must use JQuery version `3.x`
* You are not allowed to use `var`
* HTML should not reload for each action: DOM manipulation, update values, fetch data…

## More Info
### Import JQuery
```
<head>
    <script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
</head>
```
### Before starting the project…
You will work on a codebase using [Flasgger](https://github.com/flasgger/flasgger), you will need to install it locally first before starting the RestAPI:
```
$ sudo apt-get install -y python3-lxml
$ sudo pip3 install flask_cors # if it was not installed yet
$ sudo pip3 install flasgger
```
If the RestAPI is not starting, please read the error message. Based on the(ses) error message(s), you will have to troubleshoot potential dependencies issues.

Here some solutions:

### `jsonschema` exception
```
$ sudo pip3 uninstall -y jsonschema 
$ sudo pip3 install jsonschema==3.0.1
```
### `No module named 'pathlib2'`
```
$ sudo pip3 install pathlib2
```
### Expose ports from your Vagrant
In your `Vagrantfile`, add this line for each port forwarded
```
# I expose the port 5001 of my vm to the port 5001 on my computer
config.vm.network :forwarded_port, guest: 5001, host: 5001
```
if you need to expose other ports, same line but you will need to replace the “guest port” (inside your vagrant) and your “host port” (outside your vagrant, used from your browser for example)

It’s important in your project, to use the AirBnB API with the port `5001`

![hbnb_step5](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/6f29991a-344f-46e1-8309-a63643d214b0)


## Tasks

[0. Last clone!](./AirBnB_clone_v4)

A new codebase again? Yes!

For this project you will fork this [codebase](https://github.com/jzamora5/AirBnB_clone_v3):

* Update the repository name to `AirBnB_clone_v4`
* Update the `README.md`:
	* Add yourself as an author of the project
	* Add new information about your new contribution
	* Make it better!
* If you’re the owner of this codebase, create a new repository called `AirBnB_clone_v4` and copy over all files from `AirBnB_clone_v3`
* If you didn’t install Flasgger from the previous project, it’s time! `sudo pip3 install flasgger`

[1. Cash only](./0-hbnb.py)

Write a script that starts a Flask web application:

* Based on `web_flask`, copy: `web_flask/static`, `web_flask/templates/100-hbnb.html`, `web_flask/__init__.py` and `web_flask/100-hbnb.py` into the `web_dynamic` folder
* Rename `100-hbnb.py` to [0-hbnb.py](./0-hbnb.py)
* Rename `100-hbnb.html` to [0-hbnb.html](./tmplates/0-hbnb.html)
* Update `0-hbnb.py` to replace the existing route to `/0-hbnb/`
 
**If `100-hbnb.html` is not present, use `8-hbnb.html` instead**

```
guillaume@ubuntu:~/AirBnB_v4$ HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db HBNB_TYPE_STORAGE=db python3 -m web_dynamic.0-hbnb
* Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
....
```
One problem now is the asset caching done by Flask.

To avoid that, you will add a query string to each asset:

In `0-hbnb.p`y, add a variable `cache_id` to the `render_template`. The value of this variable must be an UUID (`uuid.uuid4()`)

In `0-hbnb.html`, add this variable `cache_id` as query string to each `<link>` tag URL
```
guillaume@ubuntu:~/AirBnB_v4$ curl -s -XGET http://0.0.0.0:5000/0-hbnb/ | head -6
<!DOCTYPE HTML>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="stylesheet" type="text/css" href="../static/styles/4-common.css?e211c9eb-7d17-4f12-85eb-4d50fa50cb1d" />
    <link rel="stylesheet" type="text/css" href="../static/styles/3-header.css?e211c9eb-7d17-4f12-85eb-4d50fa50cb1d" />
guillaume@ubuntu:~/AirBnB_v4$ curl -s -XGET http://0.0.0.0:5000/0-hbnb/ | head -6
<!DOCTYPE HTML>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="stylesheet" type="text/css" href="../static/styles/4-common.css?f834413e-0aa9-4767-b64a-c92db9cb1f82" />
    <link rel="stylesheet" type="text/css" href="../static/styles/3-header.css?f834413e-0aa9-4767-b64a-c92db9cb1f82" />
guillaume@ubuntu:~/AirBnB_v4$
```
![Screenshot from 2023-08-04 20-43-02](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/951b4eda-a040-4ec2-b8af-6026bed453a5)

![Screenshot from 2023-08-04 20-43-22](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/25a0722e-4348-46dc-bee4-ff62ae21e019)

![Screenshot from 2023-08-04 20-43-17](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/efad3f10-b7e5-4ea9-94ba-74a92e0fb058)

[2. Select some Amenities to be comfortable!](./1-hbnb.py)

For the moment the filters section is static, let’s make it dynamic!

Replace the route `0-hbnb` with `1-hbnb` in the file `1-hbnb.py` (based on `0-hbnb.py`)

Create a new template `1-hbnb.html` (based on `0-hbnb.html`) and update it:

* Import JQuery in the `<head>` tag
* Import the JavaScript `static/scripts/1-hbnb.js` in the `<head>` tag
	* In `1-hbnb.html` and the following HTML files, add this variable cache_id as query string to the above `<script>` tag
* Add a `<input type="checkbox">` tag to the `li` tag of each `amenity`
* The new checkbox must be at `10px` on the left of the `Amenity` name
* Add to the `input` tags of each amenity (`<li>` tag) the attribute `data-id=":amenity_id"` => this will allow us to retrieve the `Amenity` ID from the DOM
* Add to the `input` tags of each `amenity` (`<li>` tag) the attribute `data-name=":amenity_name"` => this will allow us to retrieve the Amenity name from the DOM

Write a JavaScript script ([static/scripts/1-hbnb.js](./static/scripts/1-hbnb.js)):

* Your script must be executed only when DOM is loaded
* You must use JQuery
* Listen for changes on each `input` checkbox tag:
	* if the checkbox is checked, you must store the Amenity ID in a variable (dictionary or list)
	* if the checkbox is unchecked, you must remove the Amenity ID from the variable
	* update the `h4` tag inside the `div` Amenities with the list of Amenities checked

As example:

![8e3c27078d62806b8ad1c1a682fbb3a48636ab89](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/9c940fc1-62a2-4e4d-a499-a5b0d8d7f821)

![4e5cecdd82a70f07cd283ef8e242ad325c95b564](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/8ca7f13f-4355-48fa-b4f4-6540a8763ebf)

![fb54e3081e229654db6e71ba919db753a791dcc3](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/7c254748-7f87-4cca-a390-074d7cc86261)

![Screenshot from 2023-08-04 21-33-35](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/d4eb8743-4c70-4fe5-b878-420e4b3f578c)

![Screenshot from 2023-08-04 21-33-22](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/52e14407-5099-4619-8a39-77c0fec6f9b3)

![Screenshot from 2023-08-04 21-33-12](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/8ff12926-d71f-4a04-bb41-b35496f3627f)

[3. API status](./2-hbnb.py)

Before requesting the HBNB API, it’s better to know the status of this one.

Update the API entry point (`api/v1/app.py`) by replacing the current CORS `CORS(app, origins="0.0.0.0")` by `CORS(app, resources={r"/api/v1/*": {"origins": "*"}})`.

Change the route `1-hbnb` to `2-hbnb` in the file `2-hbnb.py` (based on `1-hbnb.py`)

Create a new template `2-hbnb.html` (based on `1-hbnb.html`) and update it:

* Import the JavaScript `static/scripts/2-hbnb.js` in the `<head>` tag (instead of `1-hbnb.js`)
* Add a new `div` element in the `header` tag:
	* Attribute ID should be `api_status`
	* Align to the right
	* Circle of `40px` diameter
	* Center vertically
	* At `30px` of the right border
	* Background color `#cccccc`
* Also add a class `available` for this new element in `web_dynamic/static/styles/3-header.css`:
	* Background color `#ff545f`

Write a JavaScript script (`static/scripts/2-hbnb.js`):

* Based on `1-hbnb.js`
* Request `http://0.0.0.0:5001/api/v1/status/`:
	* If in the status is “OK”, add the class `available` to the `div#api_status`
	* Otherwise, remove the class `available` to the `div#api_status`

To start the API in the port `5001`:
```
guillaume@ubuntu:~/AirBnB_v4$ HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db HBNB_TYPE_STORAGE=db HBNB_API_PORT=5001 python3 -m api.v1.app
...
```
For example:

![Screenshot from 2023-08-04 22-04-30](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/bee457ba-76b8-4715-a159-f74cbd13a41f)

[4. Fetch places](./3-hbnb.py)

Replace the route `2-hbnb` with `3-hbnb` in the file `3-hbnb.py` (based on `2-hbnb.py`)

Create a new template `3-hbnb.html` (based on `2-hbnb.html`) and update it:

* Import the JavaScript `static/scripts/3-hbnb.js` in the `<head>` tag (instead of `2-hbnb.js`)
* Remove the entire Jinja section of displaying all places (all `article` tags)

Write a JavaScript script (`static/scripts/3-hbnb.js`):

* Based on `2-hbnb.js`
* Request `http://0.0.0.0:5001/api/v1/places_search/`:
	* Description of this endpoint here. **If this endpoint is not available, you will have to add it to the API** (you can work all together for creating this endpoint)
	* Send a `POST` request with `Content-Type: application/json` and an empty dictionary in the body - cURL version: `curl "http://0.0.0.0:5001/api/v1/places_search" -XPOST -H "Content-Type: application/json" -d '{}'`
	* Loop into the result of the request and create an `article` tag representing a `Place` in the `section.places`. (you can remove the Owner tag in the place description)

The final result must be the same as previously, but now, places are loaded from the front-end, not from the back-end!

![Screenshot from 2023-08-04 22-27-46](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/a20074c5-8e81-4df6-80c7-3523081bef3d)

[5. Filter places by Amenity](./4-hbnb.py)

Replace the route `3-hbnb` with `4-hbnb` in the file `4-hbnb.py` (based on `3-hbnb.py`)

Create a new template `4-hbnb.html` (based on `3-hbnb.html`) and update it:

* Import the JavaScript `static/scripts/4-hbnb.js` in the `<head>` tag (instead of `3-hbnb.js`)
Write a JavaScript script (`static/scripts/4-hbnb.js`):

* Based on `3-hbnb.js`
* When the `button` tag is clicked, a new POST request to `places_search` should be made with the list of `Amenities` checked

Now you have the first filter implemented, enjoy!

![Screenshot from 2023-08-04 22-39-14](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/04a9dce4-ef40-46ee-8707-9446560a7417)

![Screenshot from 2023-08-04 22-39-32](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/fab97ca4-83a9-4f30-b6e9-5eaaaff04905)

![Screenshot from 2023-08-04 22-40-12](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/b4eb86f3-4a3e-4ca5-ae64-a9711a8c2527)

[6. States and Cities](./100-hbnb.py)

Now, reproduce the same steps with the `State` and `City` filter:

Replace the route `4-hbnb` to `100-hbnb` in the file `100-hbnb.py` (based on `4-hbnb.py`)

Create a new template `100-hbnb.html` (based on `4-hbnb.html`) and update it:

* Import the JavaScript `static/scripts/100-hbnb.js` in the `<head>` tag (instead of `4-hbnb.js`)
* Add to all `li` tags of each `state` a new tag: `<input type="checkbox">`
* Add to all `li` tags of each `cities` a new tag: `<input type="checkbox">`
* The new checkbox must be at `10px` on the left of the `State` or `City` name
* Add to all `input` tags of each states (`<li>` tag) the attribute `data-id=":state_id"`
* Add to all `input` tags of each states (`<li>` tag) the attribute `data-name=":state_name"`
* Add to all `input` tags of each cities (`<li>` tag) the attribute `data-id=":city_id"`
* Add to all `input` tags of each cities (`<li>` tag) the attribute `data-name=":city_name"`

Write a JavaScript script (`static/scripts/100-hbnb.js`):

* Based on `4-hbnb.js`
* Listen to changes on each `input` checkbox tag:
	* if the checkbox is checked, you must store the `State` or `City` ID in a variable (dictionary or list)
	* if the checkbox is unchecked, you must remove the `State` or `City` ID from the variable
	* update the `h4` tag inside the `div` Locations with the list of `States` or `Cities` checked
* When the `button` tag is clicked, a new POST request to `places_search` should be made with the list of `Amenities`, `Cities` and `States` checked

![Screenshot from 2023-08-04 22-56-29](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/0045b3c6-6023-41ff-a457-a187c7d3aea9)

![Screenshot from 2023-08-04 22-56-43](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/a594fde4-97c7-4b96-9f9f-35c78c80d9b5)

[7. Reviews](./101-hbnb.py)

Let’s add a new feature: show and hide reviews!

Replace the route `100-hbnb` to `101-hbnb` in the file `101-hbnb.py` (based on `100-hbnb.py`)

Create a new template `101-hbnb.html` (based on `100-hbnb.html`) and update it:

* Import the JavaScript `static/scripts/101-hbnb.js` in the `<head>` tag (instead of `101-hbnb.js`)
* Design the list of reviews from this task
* Add a `span` element at the right of the `H2` “Reviews” with value “show” (add all necessary attributes to do this feature)

Write a JavaScript script (`static/scripts/101-hbnb.js`):

* Based on `100-hbnb.js`
* When the `span` next to the Reviews `h2` is clicked by the user:
	* Fetch, parse, display reviews and change the text to “`hide`”
	* If the text is “`hide`”: remove all Review elements from the DOM
	* This button should work like a toggle to fetch/display and hide reviews

![Screenshot from 2023-08-04 23-15-07](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/8b190396-e079-4b60-bff7-69b2ecfc71b9)

![Screenshot from 2023-08-04 23-15-34](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/dec572ef-166e-4b29-b03d-8535f2721ec6)

![Screenshot from 2023-08-04 23-15-44](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/aca73aab-9772-4aa9-8dba-95476400ac9d)

![Screenshot from 2023-08-04 23-15-49](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/186ef760-704c-4f48-afac-13144b1a4e89)

![Screenshot from 2023-08-04 23-16-21](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/aa4e396a-95dd-4f67-be00-caaa3f3b1805)

![Screenshot from 2023-08-04 23-16-27](https://github.com/achrafkassimi/AirBnB_clone_v4/assets/85158665/eb5b133b-ccfd-42ef-acdc-f8751c1fbfc5)