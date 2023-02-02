# simple test code for python + Flask + AJAX call with JSON

Sources: 
- https://towardsdatascience.com/using-python-flask-and-ajax-to-pass-information-between-the-client-and-server-90670c64d688
- https://www.makeuseof.com/tag/python-javascript-communicate-json/

## Setup

```
# I'm using python 3.10
# need flask and cors library
pip install Flask flask-cors
```

## Workflow

* Start the server:

```
python app.py

 * Serving Flask app 'app'
 * Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on http://127.0.0.1:5000
```

* Point your browser to the URL given: http://127.0.0.1:5000

  This will call the `app.route('/')` defined in the app, which grabs
  the `templates/index.html` file, replaces some of the file paths, and
  sends it back to the browser. The browser will follow up with requests
  for the CSS and JS files found in the static directory.

* Enter some data into the form. e.g. Height = 69 (5'9") and Weight = 165.

* Click Next

  This calls the function defined in the `static/bmi-calc.js` file.
  It pulls the form data from the document and puts it into a javascript
  variable `post_data`. It then uses jquery to encode the data as JSON
  and POST it to the route in the python app.

  The `app.route('/process_bmi')` in app.py read the POST'ed JSON data
  into a python variable. It then does the BMI calculation and categorization
  and puts those results into a new variable. Finally it returns the
  results encoded as JSON again.

  When the AJAX function gets the results back successfully, it uses
  the data to update the HTML page with the values.

* Hit Ctrl-C to kill the running app.py when finished.
