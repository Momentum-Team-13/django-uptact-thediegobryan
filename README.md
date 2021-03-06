# Uptact

This is your first Django project. For this project, functionality has already been added to this sample Django application. You will add new functionality throughout the project in order to better understand how all the pieces of Django work together.

## Getting this project set up

You must have [Pipenv](https://pipenv.pypa.io/en/latest/) installed. This will allow you to get all dependencies of this project installed on your computer. You should already have Pipenv installed already.

To check, run:

```sh
pipenv --version
```

If you get a "command not found" message, run the following:

```sh
pip install pipenv
```

Once you ensure you have Pipenv installed, run the following command inside this project's directory:

```
pipenv install
```

Pipenv uses a concept called a "virtualenv" in order to isolate the dependencies of this project from any other project. This requires you to run a command when you want to start working on this project. Before working on the project, run:

```
pipenv shell
```

This will change your terminal to use the virtualenv for this project. _You must run this command in any new terminal you open._ You will know if you are in the virtualenv because your prompt will change to show you. You should have the name of the virtualenv on your prompt, like the following:

```
django--uptact on  main via 🐍 v3.10.0 (django--uptact)
❯
```

Note what is in parens at the end -- that's the name of the virtualenv. It shows in the prompt when you are "inside" that virtual environment.

If you need to exit the virtualenv, simply close your terminal window or run `exit`.

If you get a `SECRET_KEY` error when you run your django server, you'll need to make sure Django can find that variable, which it is looking for in a `.env` file in the `uptact` project directory (see `django-environ` below). You should create a `.env` file inside the `uptact` project directory. This repo provides a `.env.sample` that you can copy.

```sh
$ cp uptact/.env.sample uptact/.env
```
💫 Remember that `cp` is the shell command to copy files.


## Task 1

For the first assignment, spend time familiarizing yourself with Django. Look at the `uptact` directory (the _project directory_) and the `contacts` directory (an _app directory_). Answer the following questions for yourself:

- If I wanted to add a new URL to this project, what two files would I edit?
    -uptact/urls.py
    -views.py
- If I wanted to add a birthday to each contact, what file would I edit?
    -contacts/models.py
Then do the following steps:
1. Add a birthday field to the `Contact` model. This field should be of type `DateField` and should be allowed to be null and empty.
<!-- line 22 birthday = models.DateField(blank=True, null=True) -->

2. Make sure you can edit the birthday by changing the `ContactForm`.
<!-- forms.py added birthday to forms -->
3. Add the ability to display the birthday on the list of contacts. You will have to edit `templates/contacts/list_contacts.html`.

When you get through that, add a birthday to one of your contacts to test out your code.

## Task 2

With this assignment, we are going to explore relationships between models, and how URLs and views work.

Answer the following questions:

- If I wanted to add a new model, where would I do that?
models.py
- If I wanted to connect the new model to the `Contact` model, how would I do that?
 forms.py is an example of this
Then do the following steps:

1. Add a new model, `Note`, to the `contacts` app. This model should contain text for the note and the date/time of the note. Look at the `auto_now_add` option for the `DateTimeField` to have the date/time automatically populated.
2. Connect the `Note` model to the `Contact` model using a `ForeignKey`.
3. Use the Django console to add a note to one of your contacts.
4. Make a new view and template to see an individual contact. The URL for this view should be `contacts/<int:pk>/`. Show the notes for that contact on this individual view. Otherwise, this page can look like an individual contact on the contacts list page.

## Task 3

With this assignment, we are going to explore forms.

Previously, you added a `Note` model, but had no ability to create new notes through your Django application. Now do the following steps:

1. Add a new form called `NoteForm`. This form should let you edit only one field, the text of the note.
2. Add a new view to accept this form via `POST` request and add a new note to a specific contact. The contact will be specified via the URL, which should be `contacts/<int:pk>/notes/`.
3. On the individual contact view that you previously added, add a form to create new notes. When the note is created, redirect back to the contact view.

Test this by adding some notes to individual contacts.

## About this project

This project makes some additions and modifications to the defaults in Django:

- There is a custom user model defined in `users.models.User`.
- There is a `templates/` and a `static/` directory at the top level, both of which are set up to be used.
- A `.gitignore` file is provided.
- [Pipenv](https://pipenv.pypa.io/en/latest/) is used to manage dependencies.

It also adds the following dependencies:

- [django-extensions](https://django-extensions.readthedocs.io/en/latest/) - adds some additional helpful django commands
- [django-debug-toolbar](https://django-debug-toolbar.readthedocs.io/en/latest/) - gives us a debugging panel in the browser
- [django-environ](https://django-environ.readthedocs.io/en/latest/) - lets us use a `.env` file to hide some of our settings. `DEBUG`, `SECRET_KEY`, and `DATABASES` settings are set by this package.
