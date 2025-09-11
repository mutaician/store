# These ae my notes that I note as I relearn Rails
To run rails app:
    bin/rails server

## Database model
Active record - maps ralational databases to ruby code, helps to generate sql for interacting with the database
To create a database model run:
    bin/rails generate model [Model_name] [column_name:type]
The command create a db migration, active record model and tests for the model
NB: model names are singular because an instatiated model represents a single record in the db

### Database migrations
Migration is a set of changes to make to the database
to run migrations:
    bin/rails db:migrate
* run bin/rails db:rollback to undo last migration

## Rails Console
interactive tool for testing code in rails app:
    bin/rails console

### Active Record model basics
1. Creating a new record: instance = Model.new(-:-) - new instance and not saved to the database
2. Save the record to the db: instance.save
3. We can use Model.create(-:-) to instantiate and save Active record object
4. To query records = Model.all
5. To filter records = Model.where(column:___)
6. To order records = Model.order(column: :direction) - valid directions: [:asc, :desc, :ASC, :DESC]
7. To find specific record by id = Model.find(id)
8. Updating records = 2 ways: using update on model instance -> instance.update(column: item), or asigning attributes and calling save
9. Deleting records = call destroy on an instance

### Validations 
to ensure data inserted into the db adheres to certain rules
    validates :column, presence: true # to presence of an item
returns false with an instance containing errors which can be known exactly by instance.errors.full_messages

## Request's journey
have a route, controller with an action and a view
a route maps requests to a controller action, the controller action performs necessary work to handle the requests and prepares any data for view, view displays data in desired format

### Routes
it determines how an incoming HTTP request is directed to the appropriate controller and action forprocessing
HTTP Methods:
1. GET -> tells a server to retrieve the data for a given URL, loading a page or fetching a record
2. POST -> submit data to url for processing,  usually creating a new record
3. PUT/PATCH -> submits data to URL to update an existing record
4. DELETE -> tells server to delete a record
in rails its line of code that pairs an HTTP method to a URL path and also whch controller and action should respond to a request
    get "/path", to: "controller#action"

Crud Routes:
    Index - Shows all the records
    New - Renders a form for creating a new record
    Create - Processes the new form submission, handling errors and creating the record
    Show - Renders a specific record for viewing
    Edit - Renders a form for updating a specific record
    Update (full) - Handles the edit form submission, handling errors and updating the entire record, and typically triggered by a PUT request.
    Update (partial) - Handles the edit form submission, handling errors and updating specific attributes of the record, and typically triggered by a PATCH request.
    Destroy - Handles deleting a specific record
to create all routes: resources :routes i'e resources :products in routes.rb

### Controllers and Actions
To generate a controller and controller:
    bin/rails generate controller <Name> <Action>, i.e --- Products index
The command creates controller itself, views folder for the controller, view file for the action we specified, test for the controller, helper  file for extracting logic in views

ERB(Embedded Ruby) - allows to execute Ruby code to dynamically generate HTML
    <%= %>, <%= debug %> print variables in yaml format to help in debugging

Route prefixes provide helpers to use for generating URLs with Ruby code
<prefix>_path returns a relative path which the browser understands for the current domain
<prefix>_url returns full  URL inlcluding protocol and host

#### Helpers
`link_to` - it accepts the display content for the link and path/URL to link to for the href attribute
`form_with` - generate html form,, handle csrf token, generate url based on model: ___ provided, tailor submit to the model
`before_action` - extract shared code between actions and run it before the action

Partials allow reusing a view in many places, _file.html.erb

### Authentication
    bin/rails generate authentication
    bin/rails db:migrate

### Caching
using `cache` method