Жылдам іске кіру
==========

Жұмысқа кірісуді күте алмайсыз ба? Бұл бет Flask туралы жақсы түсінік береді.
Жобаны орнату және алдымен Flask орнату үшін :doc: `installation` тармағын орындаңыз.


Минималды қолдану
---------------------

Минималды Flask қосымшасы келесідей көрінеді:

.. code-block:: python

    from flask import Flask

    app = Flask(__name__)

    @app.route("/")
    def hello_world():
        return "<p>Hello, World!</p>"

Сонымен, Бұл код не істеді?

1. Алдымен біз импорттадық: :class:`~flask.Flask` классты. Бұл класстың данасы біздің wsgi қосымшасы болады.
2. Әрі қарай, біз осы класстың данасын жасаймыз. Бірінші аргумент-модульдің немесе қолданба бумасының атауы. ``__name__`` - бұл көптеген жағдайларға сәйкес келетін ыңғайлы төте жол. Бұл Flask шаблондар мен статикалық файлдар сияқты ресурстарды қайдан іздеу керектігін білуі үшін қажет.
3. Содан кейін біз  :meth:`~flask.Flask.route`  деген декоратор қолданамыз. Бұл Flask-ке біздің функцияны қандай URL іске қосуы керектігін айтады.
4. Функция пайдаланушының шолғышында көрсеткіміз келетін хабарды қайтарады. Әдепкі мазмұн түрі-HTML, сондықтан жолдағы HTML браузерде көрсетіледі.

Оны :file:`hello.py` - немесе ұқсас атаулармен сақтаңыз. Қолданбаны :file:`flask.py` - атымен сақтамауын назар аударыңыз, өйткені бұл Flask-тің өзіне атаулар қақтығысы боп келеді.

Қолданбаны іске қосу үшін ``flask``пәрменін немесе ``python -m flask`` қолданыңыз.
``--app`` опциясын пайдаланып, flask-ке қолданбаңыздың қай жерде екенін айту керек.

.. code-block:: text

    $ flask --app hello run
     * Serving Flask app 'hello'
     * Running on http://127.0.0.1:5000 (Press CTRL+C to quit)

.. admonition:: Қолданбаны анықтау әрекеті

    Егер файл ``app.py`` немесе ``wsgi.py``  аталған болса,  сізге ``--app`` қолданудың қажеті жоқ. 
    Қосымша ақпарат алу үшін :doc:`/cli` қараңыз.

Бұл өте қарапайым кіріктірілген серверді іске қосады, ол тестілеуге жеткілікті, бірақ сіз өндірісте қолданғыңыз келмейтін шығар. Орналастыру параметрлері келесі бөлімде берілген :doc:`deploying/index`.

Енді http://127.0.0.1:5000 / адреске барып сіз hello world сәлемдесуін көруіңіз керек.

Егер басқа бағдарлама 5000 портын қолданып жатса, сіз серверді іске қосқан кезде ``OSError: [WinError 10013]`` немесе ``OSError: [Errno 98]`` көресіз. :ref:`address-already-in-use` көріп, онымен қалай күресуге болады.

.. _public-server:

.. admonition:: Сырттан көрінетін Сервер

  Егер сіз серверді іске қоссаңыз, серверге желідегі кез келген басқа компьютерден емес, тек өз компьютеріңізден кіруге болатынын байқайсыз.  Бұл әдепкі болып табылады, өйткені күйін келтіру режимінде қолданба пайдаланушысы компьютерде ерікті Python кодын орындай алады.

   Егер сізде отладчик өшірілген болса немесе желі пайдаланушыларына сенсеңіз, пәрмен жолына  ``--host=0.0.0.0`` қосу арқылы серверді жалпыға қол жетімді ете аласыз::

       $ flask run --host=0.0.0.0

  Бұл сіздің операциялық жүйеңізге барлық жалпыға ортақ IP мекенжайларын тыңдауды көрсетеді.

Жөндеу режимі
----------

 ``flask run``  командасы әзірлеу серверін іске қосудан гөрі көп нәрсе істей алады. Күйін келтіру режимін қосу арқылы код өзгерген кезде сервер автоматты түрде қайта жүктеледі және сұрау кезінде қате пайда болса, шолғышта интерактивті күйін келтірушіні көрсетеді.

.. image:: _static/debugger.png
    :align: center
    :class: screenshot
    :alt: The interactive debugger in action.

.. warning::

   Отладчик браузерден Python - да ерікті кодты орындауға мүмкіндік береді. Ол pin кодымен қорғалған, бірақ бәрібір қауіпсіздікке үлкен қауіп төндіреді. Өндірістік ортада әзірлеу серверін немесе отладчикті іске қоспаңыз.

Жөндеу режимін қосу үшін ``--debug`` опциясын пайдаланыңыз.

.. code-block:: text

    $ flask --app hello run --debug
     * Serving Flask app 'hello'
     * Debug mode: on
     * Running on http://127.0.0.1:5000 (Press CTRL+C to quit)
     * Restarting with stat
     * Debugger is active!
     * Debugger PIN: nnn-nnn-nnn

Мұны да қараңыз:

-   :doc:`/server` and :doc:`/cli` күйін келтіру режимінде іске қосу туралы ақпарат алу үшін.
-   :doc:`/debugging`  кірістірілген отладчикті және басқа отладчиктерді пайдалану туралы ақпарат алу үшін.
-   :doc:`/logging` and :doc:`/error handling`  қателерді тіркеу және әдемі қате беттерін көрсету үшін.


HTML-ден шығу
-------------

HTML (Flask-те әдепкі жауап түрі) қайтарылған кезде, инъекциялық шабуылдардан қорғау үшін пайдаланушының шығыс деректерінде көрсетілген кез келген мәндері қорғалған болуы керек. Кейінірек ұсынылған Jinja көмегімен көрсетілген HTML шаблондары мұны автоматты түрде жасайды.

Мұнда көрсетілген   :func:`~markupsafe.escape`  қолмен пайдалануға болады.
Көптеген мысалдарда бұл қысқаша қабылданбайды, бірақ сіз әрқашан сенімсіз деректерді қалай пайдаланатыныңызды білуіңіз керек.

.. code-block:: python

    from markupsafe import escape

    @app.route("/<name>")
    def hello(name):
        return f"Hello, {escape(name)}!"

Егер пайдаланушы ``<script>alert("bad")</script>`` атауын жібере алса, экрандау сценарийді пайдаланушының шолғышында іске қосудың орнына оны мәтін ретінде көрсетуге әкеледі.

маршруттағы ``<name>`` URL мекенжайынан мәнді алады және оны қарау функциясына жібереді. Бұл айнымалы ережелер төменде түсіндіріледі.

Маршруттау
-------

Заманауи веб-қосымшалар пайдаланушыларға көмектесу үшін мағыналы URL мекенжайларын пайдаланады. Пайдаланушылар бетті ұнатуы ықтимал және егер олар бетте есте сақтай алатын және бетке тікелей кіру үшін пайдалана алатын мағыналы URL мекенжайын пайдаланса, олар қайтып оралады.

функцияны URL мекенжайына байланыстыру үшін :meth:`~flask.Flask.route`  декораторды пайдаланыңыз. ::

@app.route('/')
    def index():
        return 'Index Page'

    @app.route('/hello')
    def hello():
        return 'Hello, World'

Сіз көп нәрсені жасай аласыз! Сіз URL бөліктерін динамикалық етіп жасай аласыз және функцияға бірнеше ережелерді қоса аласыз.

Айнымалы ережелер
``````````````

URL мекенжайына айнымалы бөлімдерді ``<variable_name>`` бөлімдерін белгілеу арқылы қосуға болады. Содан кейін сіздің функцияңыз кілт сөз аргументі ретінде ``<variable_name>``  алады. Қажет болса, дәлел түрін көрсету үшін түрлендіргішті пайдалануға болады, мысалы ``<converter:variable_name>``. ::

    from markupsafe import escape

    @app.route('/user/<username>')
    def show_user_profile(username):
        # сол пайдаланушы үшін пайдаланушы профилін көрсету
        return f'User {escape(username)}'

    @app.route('/post/<int:post_id>')
    def show_post(post_id):
        # берілген идентификатормен хабарламаны көрсету, идентификатор бүтін сан болып табылады
        return f'Post {post_id}'

    @app.route('/path/<path:subpath>')
    def show_subpath(subpath):
        # /path/ кейін ішкі жолды көрсету
        return f'Subpath {escape(subpath)}'

Түрлендіргіштердің түрлері:

========== ==========================================
``string``  (default) кез-келген мәтінді қиғаш сызықсыз қабылдайды
``int``     бүтін оң сандарды қабылдайды
``float``   оң өзгермелі нүкте мәндерін қабылдайды
``float``   ``string`` ұқсас бірақ сонымен бірге қиғаш сызықтарды қабылдайды
``uuid``    UUID жолдарын қабылдайды
========== ==========================================


Бірегей URL мекенжайлары / Қайта бағыттау әрекеті
``````````````````````````````````

Келесі екі ереже соңғы қиғаш сызықты қолданумен ерекшеленеді. ::

    @app.route('/projects/')
    def projects():
        return 'The project page'

    @app.route('/about')
    def about():
        return 'The about page'

``projects`` соңғы нүктесінің канондық URL мекенжайының соңында қиғаш сызық бар. Бұл файлдық жүйедегі қалта сияқты. Егер сіз соңында қиғаш сызығы жоқ URL мекенжайына жүгінсеңіз (``/projects``), Flask сізді соңында қиғаш сызығы бар канондық URL мекенжайына бағыттайды (``/projects``).

 ``about`` соңғы нүктесінің канондық URL мекенжайында соңғы қиғаш сызық жоқ. Бұл файл жолына ұқсас. Соңында қиғаш сызығы бар URL мекенжайына кіру(``/about/``) 404 "Not Found" қатесіне әкеледі. Бұл поискl мекенжайларын осы ресурстарға ғана тән етіп сақтауға көмектеседі, бұл іздеу жүйелеріне бір бетті екі рет индекстеуден аулақ болуға көмектеседі.


.. _url-building:

URL мекенжайын жасау
````````````

Белгілі бір функция үшін URL жасау үшін :func:`~flask.url_for` функциясын қолданыңыз. Ол функцияның атауын өзінің алғашқы аргументі ретінде және әрқайсысы URL ережесінің айнымалы бөлігіне сәйкес келетін кілт сөз аргументтерінің кез келген санын қабылдайды. Айнымалылардың белгісіз бөліктері URL мекенжайына сұрау параметрлері ретінде қосылады.

Неліктен URL мекенжайын  өз үлгілерінде қатаң кодтаудың орнына :func:`~flask.url_for` өзгерту функциясын пайдаланып URL мекенжайларын жасағыңыз келедi?

1. Реверсия көбінесе URL мекенжайларын қатаң кодтауға қарағанда айқынырақ болады.
2. Қатты бағдарламаланған URL мекенжайларын қолмен өзгерту қажеттілігін есте сақтаудың орнына URL мекенжайларын бір уақытта өзгертуге болады.
3. URL мекенжайын құру арнайы таңбаларды қорғауды мөлдір түрде өңдейді.
4. Жасалған жолдар әрқашан абсолютті болып табылады, бұл браузерлердегі салыстырмалы жолдардың күтпеген әрекетін болдырмайды.
5. Егер сіздің қосымшаңыз URL мекен-жайының түбірлік каталогынан тыс орналастырылған болса, мысалы, ``/``/my application`` орнына ``/``,  :func:`~flask.url_for` мұны сіз үшін дұрыс өңдейді.

Мысалы, мұнда біз :meth:`~flask.Flask.test_request_context` әдісін қолданып көреміз :func:`~flask.url_for`. :meth:`~flask.Flask.test_request_context. Flask-ке Python қабығын қолданған кезде де сұрауды өңдейтін сияқты әрекет етуді айтады. Қараңыз :ref:`context-locals`.

.. code-block:: python

    from flask import url_for

    @app.route('/')
    def index():
        return 'index'

    @app.route('/login')
    def login():
        return 'login'

    @app.route('/user/<username>')
    def profile(username):
        return f'{username}\'s profile'

    with app.test_request_context():
        print(url_for('index'))
        print(url_for('login'))
        print(url_for('login', next='/'))
        print(url_for('profile', username='John Doe'))

.. code-block:: text

    /
    /login
    /login?next=/
    /user/John%20Doe


HTTP әдістері
````````````

Веб-қосымшалар URL мекенжайларына кірген кезде әртүрлі HTTP әдістерін қолданады. Flask-пен жұмыс істеу кезінде HTTP әдістерімен танысу керек. Әдепкі бойынша, маршрут тек``GET`` сұрауларына жауап береді. Сіз  әр түрлі HTTP әдістерін өңдеуге арналған маршрут :meth:`~flask.Flask.route` Декоратортын ``methods`` аргументін пайдалана аласыз.
::

    from flask import request

    @app.route('/login', methods=['GET', 'POST'])
    def login():
        if request.method == 'POST':
            return do_the_login()
        else:
            return show_the_login_form()

Жоғарыдағы мысалда маршруттың барлық әдістері бір функцияда сақталады, бұл әрбір бөлік кейбір жалпы деректерді пайдаланса пайдалы болуы мүмкін.

Сондай-ақ, әртүрлі әдістерге арналған көріністерді әртүрлі функцияларға бөлуге болады. Flask келесі маршруттарды жобалау үшін төте жолды ұсынады:  :meth:`~flask.Flask.get` ,   :meth:`~flask.Flask.get` және т. б. әрбір жалпы HTTP әдісі үшін.

.. code-block:: python

    @app.get('/login')
    def login_get():
        return show_the_login_form()

    @app.post('/login')
    def login_post():
        return do_the_login()

Егер ``GET`` болса, Flask автоматты түрде  ``HEAD`` әдісін қолдайды және   `HTTP RFC`_ сәйкес  ``HEAD`` сұрауларын өңдейді. Сол сияқты,  ``OPTIONS`` сіз үшін автоматты түрде жүзеге асырылады.

.. _HTTP RFC: https://www.ietf.org/rfc/rfc2068.txt

Статикалық файлдар
------------

Динамикалық веб-қосымшаларға статикалық файлдар қажет. Әдетте CSS және JavaScript файлдары сол жерден алынады. Ең дұрысы, сіздің веб-серверіңіз сізге қызмет ету үшін конфигурацияланған, бірақ оны әзірлеу кезінде Flask жасай алады. Тек қалтаны жасаңыз :file:`static`пакетте немесе модульдің жанында`static` және ол қолданбадағы ``/static`` мекенжайында қол жетімді болады.

Статикалық файлдар үшін URL мекенжайларын жасау үшін арнайы ``'static'`` соңғы нүкте атауын пайдаланыңыз::

    url_for('static', filename='style.css')

Файл файлдық жүйеде келесідей сақталуы керек: :file:`static/style.css`.

Rendering Templates
-------------------

Generating HTML from within Python is not fun, and actually pretty
cumbersome because you have to do the HTML escaping on your own to keep
the application secure.  Because of that Flask configures the `Jinja2
<https://palletsprojects.com/p/jinja/>`_ template engine for you automatically.

Templates can be used to generate any type of text file. For web applications, you'll
primarily be generating HTML pages, but you can also generate markdown, plain text for
emails, and anything else.

For a reference to HTML, CSS, and other web APIs, use the `MDN Web Docs`_.

.. _MDN Web Docs: https://developer.mozilla.org/

To render a template you can use the :func:`~flask.render_template`
method.  All you have to do is provide the name of the template and the
variables you want to pass to the template engine as keyword arguments.
Here's a simple example of how to render a template::

    from flask import render_template

    @app.route('/hello/')
    @app.route('/hello/<name>')
    def hello(name=None):
        return render_template('hello.html', name=name)

Flask will look for templates in the :file:`templates` folder.  So if your
application is a module, this folder is next to that module, if it's a
package it's actually inside your package:

**Case 1**: a module::

    /application.py
    /templates
        /hello.html

**Case 2**: a package::

    /application
        /__init__.py
        /templates
            /hello.html

For templates you can use the full power of Jinja2 templates.  Head over
to the official `Jinja2 Template Documentation
<https://jinja.palletsprojects.com/templates/>`_ for more information.

Here is an example template:

.. sourcecode:: html+jinja

    <!doctype html>
    <title>Hello from Flask</title>
    {% if name %}
      <h1>Hello {{ name }}!</h1>
    {% else %}
      <h1>Hello, World!</h1>
    {% endif %}

Inside templates you also have access to the :data:`~flask.Flask.config`,
:class:`~flask.request`, :class:`~flask.session` and :class:`~flask.g` [#]_ objects
as well as the :func:`~flask.url_for` and :func:`~flask.get_flashed_messages` functions.

Templates are especially useful if inheritance is used.  If you want to
know how that works, see :doc:`patterns/templateinheritance`. Basically
template inheritance makes it possible to keep certain elements on each
page (like header, navigation and footer).

Automatic escaping is enabled, so if ``name`` contains HTML it will be escaped
automatically.  If you can trust a variable and you know that it will be
safe HTML (for example because it came from a module that converts wiki
markup to HTML) you can mark it as safe by using the
:class:`~markupsafe.Markup` class or by using the ``|safe`` filter in the
template.  Head over to the Jinja 2 documentation for more examples.

Here is a basic introduction to how the :class:`~markupsafe.Markup` class works::

    >>> from markupsafe import Markup
    >>> Markup('<strong>Hello %s!</strong>') % '<blink>hacker</blink>'
    Markup('<strong>Hello &lt;blink&gt;hacker&lt;/blink&gt;!</strong>')
    >>> Markup.escape('<blink>hacker</blink>')
    Markup('&lt;blink&gt;hacker&lt;/blink&gt;')
    >>> Markup('<em>Marked up</em> &raquo; HTML').striptags()
    'Marked up » HTML'

.. versionchanged:: 0.5

   Autoescaping is no longer enabled for all templates.  The following
   extensions for templates trigger autoescaping: ``.html``, ``.htm``,
   ``.xml``, ``.xhtml``.  Templates loaded from a string will have
   autoescaping disabled.

.. [#] Unsure what that :class:`~flask.g` object is? It's something in which
   you can store information for your own needs. See the documentation
   for :class:`flask.g` and :doc:`patterns/sqlite3`.


Accessing Request Data
----------------------

For web applications it's crucial to react to the data a client sends to
the server.  In Flask this information is provided by the global
:class:`~flask.request` object.  If you have some experience with Python
you might be wondering how that object can be global and how Flask
manages to still be threadsafe.  The answer is context locals:


.. _context-locals:

Context Locals
``````````````

.. admonition:: Insider Information

   If you want to understand how that works and how you can implement
   tests with context locals, read this section, otherwise just skip it.

Certain objects in Flask are global objects, but not of the usual kind.
These objects are actually proxies to objects that are local to a specific
context.  What a mouthful.  But that is actually quite easy to understand.

Imagine the context being the handling thread.  A request comes in and the
web server decides to spawn a new thread (or something else, the
underlying object is capable of dealing with concurrency systems other
than threads).  When Flask starts its internal request handling it
figures out that the current thread is the active context and binds the
current application and the WSGI environments to that context (thread).
It does that in an intelligent way so that one application can invoke another
application without breaking.

So what does this mean to you?  Basically you can completely ignore that
this is the case unless you are doing something like unit testing.  You
will notice that code which depends on a request object will suddenly break
because there is no request object.  The solution is creating a request
object yourself and binding it to the context.  The easiest solution for
unit testing is to use the :meth:`~flask.Flask.test_request_context`
context manager.  In combination with the ``with`` statement it will bind a
test request so that you can interact with it.  Here is an example::

    from flask import request

    with app.test_request_context('/hello', method='POST'):
        # now you can do something with the request until the
        # end of the with block, such as basic assertions:
        assert request.path == '/hello'
        assert request.method == 'POST'

The other possibility is passing a whole WSGI environment to the
:meth:`~flask.Flask.request_context` method::

    with app.request_context(environ):
        assert request.method == 'POST'

The Request Object
``````````````````

The request object is documented in the API section and we will not cover
it here in detail (see :class:`~flask.Request`). Here is a broad overview of
some of the most common operations.  First of all you have to import it from
the ``flask`` module::

    from flask import request

The current request method is available by using the
:attr:`~flask.Request.method` attribute.  To access form data (data
transmitted in a ``POST`` or ``PUT`` request) you can use the
:attr:`~flask.Request.form` attribute.  Here is a full example of the two
attributes mentioned above::

    @app.route('/login', methods=['POST', 'GET'])
    def login():
        error = None
        if request.method == 'POST':
            if valid_login(request.form['username'],
                           request.form['password']):
                return log_the_user_in(request.form['username'])
            else:
                error = 'Invalid username/password'
        # the code below is executed if the request method
        # was GET or the credentials were invalid
        return render_template('login.html', error=error)

What happens if the key does not exist in the ``form`` attribute?  In that
case a special :exc:`KeyError` is raised.  You can catch it like a
standard :exc:`KeyError` but if you don't do that, a HTTP 400 Bad Request
error page is shown instead.  So for many situations you don't have to
deal with that problem.

To access parameters submitted in the URL (``?key=value``) you can use the
:attr:`~flask.Request.args` attribute::

    searchword = request.args.get('key', '')

We recommend accessing URL parameters with `get` or by catching the
:exc:`KeyError` because users might change the URL and presenting them a 400
bad request page in that case is not user friendly.

For a full list of methods and attributes of the request object, head over
to the :class:`~flask.Request` documentation.


File Uploads
````````````

You can handle uploaded files with Flask easily.  Just make sure not to
forget to set the ``enctype="multipart/form-data"`` attribute on your HTML
form, otherwise the browser will not transmit your files at all.

Uploaded files are stored in memory or at a temporary location on the
filesystem.  You can access those files by looking at the
:attr:`~flask.request.files` attribute on the request object.  Each
uploaded file is stored in that dictionary.  It behaves just like a
standard Python :class:`file` object, but it also has a
:meth:`~werkzeug.datastructures.FileStorage.save` method that
allows you to store that file on the filesystem of the server.
Here is a simple example showing how that works::

    from flask import request

    @app.route('/upload', methods=['GET', 'POST'])
    def upload_file():
        if request.method == 'POST':
            f = request.files['the_file']
            f.save('/var/www/uploads/uploaded_file.txt')
        ...

If you want to know how the file was named on the client before it was
uploaded to your application, you can access the
:attr:`~werkzeug.datastructures.FileStorage.filename` attribute.
However please keep in mind that this value can be forged
so never ever trust that value.  If you want to use the filename
of the client to store the file on the server, pass it through the
:func:`~werkzeug.utils.secure_filename` function that
Werkzeug provides for you::

    from werkzeug.utils import secure_filename

    @app.route('/upload', methods=['GET', 'POST'])
    def upload_file():
        if request.method == 'POST':
            file = request.files['the_file']
            file.save(f"/var/www/uploads/{secure_filename(file.filename)}")
        ...

For some better examples, see :doc:`patterns/fileuploads`.

Cookies
```````

To access cookies you can use the :attr:`~flask.Request.cookies`
attribute.  To set cookies you can use the
:attr:`~flask.Response.set_cookie` method of response objects.  The
:attr:`~flask.Request.cookies` attribute of request objects is a
dictionary with all the cookies the client transmits.  If you want to use
sessions, do not use the cookies directly but instead use the
:ref:`sessions` in Flask that add some security on top of cookies for you.

Reading cookies::

    from flask import request

    @app.route('/')
    def index():
        username = request.cookies.get('username')
        # use cookies.get(key) instead of cookies[key] to not get a
        # KeyError if the cookie is missing.

Storing cookies::

    from flask import make_response

    @app.route('/')
    def index():
        resp = make_response(render_template(...))
        resp.set_cookie('username', 'the username')
        return resp

Note that cookies are set on response objects.  Since you normally
just return strings from the view functions Flask will convert them into
response objects for you.  If you explicitly want to do that you can use
the :meth:`~flask.make_response` function and then modify it.

Sometimes you might want to set a cookie at a point where the response
object does not exist yet.  This is possible by utilizing the
:doc:`patterns/deferredcallbacks` pattern.

For this also see :ref:`about-responses`.

Redirects and Errors
--------------------

To redirect a user to another endpoint, use the :func:`~flask.redirect`
function; to abort a request early with an error code, use the
:func:`~flask.abort` function::

    from flask import abort, redirect, url_for

    @app.route('/')
    def index():
        return redirect(url_for('login'))

    @app.route('/login')
    def login():
        abort(401)
        this_is_never_executed()

This is a rather pointless example because a user will be redirected from
the index to a page they cannot access (401 means access denied) but it
shows how that works.

By default a black and white error page is shown for each error code.  If
you want to customize the error page, you can use the
:meth:`~flask.Flask.errorhandler` decorator::

    from flask import render_template

    @app.errorhandler(404)
    def page_not_found(error):
        return render_template('page_not_found.html'), 404

Note the ``404`` after the :func:`~flask.render_template` call.  This
tells Flask that the status code of that page should be 404 which means
not found.  By default 200 is assumed which translates to: all went well.

See :doc:`errorhandling` for more details.

.. _about-responses:

About Responses
---------------

The return value from a view function is automatically converted into
a response object for you. If the return value is a string it's
converted into a response object with the string as response body, a
``200 OK`` status code and a :mimetype:`text/html` mimetype. If the
return value is a dict or list, :func:`jsonify` is called to produce a
response. The logic that Flask applies to converting return values into
response objects is as follows:

1.  If a response object of the correct type is returned it's directly
    returned from the view.
2.  If it's a string, a response object is created with that data and
    the default parameters.
3.  If it's an iterator or generator returning strings or bytes, it is
    treated as a streaming response.
4.  If it's a dict or list, a response object is created using
    :func:`~flask.json.jsonify`.
5.  If a tuple is returned the items in the tuple can provide extra
    information. Such tuples have to be in the form
    ``(response, status)``, ``(response, headers)``, or
    ``(response, status, headers)``. The ``status`` value will override
    the status code and ``headers`` can be a list or dictionary of
    additional header values.
6.  If none of that works, Flask will assume the return value is a
    valid WSGI application and convert that into a response object.

If you want to get hold of the resulting response object inside the view
you can use the :func:`~flask.make_response` function.

Imagine you have a view like this::

    from flask import render_template

    @app.errorhandler(404)
    def not_found(error):
        return render_template('error.html'), 404

You just need to wrap the return expression with
:func:`~flask.make_response` and get the response object to modify it, then
return it::

    from flask import make_response

    @app.errorhandler(404)
    def not_found(error):
        resp = make_response(render_template('error.html'), 404)
        resp.headers['X-Something'] = 'A value'
        return resp


APIs with JSON
``````````````

A common response format when writing an API is JSON. It's easy to get
started writing such an API with Flask. If you return a ``dict`` or
``list`` from a view, it will be converted to a JSON response.

.. code-block:: python

    @app.route("/me")
    def me_api():
        user = get_current_user()
        return {
            "username": user.username,
            "theme": user.theme,
            "image": url_for("user_image", filename=user.image),
        }

    @app.route("/users")
    def users_api():
        users = get_all_users()
        return [user.to_json() for user in users]

This is a shortcut to passing the data to the
:func:`~flask.json.jsonify` function, which will serialize any supported
JSON data type. That means that all the data in the dict or list must be
JSON serializable.

For complex types such as database models, you'll want to use a
serialization library to convert the data to valid JSON types first.
There are many serialization libraries and Flask API extensions
maintained by the community that support more complex applications.


.. _sessions:

Sessions
--------

In addition to the request object there is also a second object called
:class:`~flask.session` which allows you to store information specific to a
user from one request to the next.  This is implemented on top of cookies
for you and signs the cookies cryptographically.  What this means is that
the user could look at the contents of your cookie but not modify it,
unless they know the secret key used for signing.

In order to use sessions you have to set a secret key.  Here is how
sessions work::

    from flask import session

    # Set the secret key to some random bytes. Keep this really secret!
    app.secret_key = b'_5#y2L"F4Q8z\n\xec]/'

    @app.route('/')
    def index():
        if 'username' in session:
            return f'Logged in as {session["username"]}'
        return 'You are not logged in'

    @app.route('/login', methods=['GET', 'POST'])
    def login():
        if request.method == 'POST':
            session['username'] = request.form['username']
            return redirect(url_for('index'))
        return '''
            <form method="post">
                <p><input type=text name=username>
                <p><input type=submit value=Login>
            </form>
        '''

    @app.route('/logout')
    def logout():
        # remove the username from the session if it's there
        session.pop('username', None)
        return redirect(url_for('index'))

.. admonition:: How to generate good secret keys

    A secret key should be as random as possible. Your operating system has
    ways to generate pretty random data based on a cryptographic random
    generator. Use the following command to quickly generate a value for
    :attr:`Flask.secret_key` (or :data:`SECRET_KEY`)::

        $ python -c 'import secrets; print(secrets.token_hex())'
        '192b9bdd22ab9ed4d12e236c78afcb9a393ec15f71bbf5dc987d54727823bcbf'

A note on cookie-based sessions: Flask will take the values you put into the
session object and serialize them into a cookie.  If you are finding some
values do not persist across requests, cookies are indeed enabled, and you are
not getting a clear error message, check the size of the cookie in your page
responses compared to the size supported by web browsers.

Besides the default client-side based sessions, if you want to handle
sessions on the server-side instead, there are several
Flask extensions that support this.

Message Flashing
----------------

Good applications and user interfaces are all about feedback.  If the user
does not get enough feedback they will probably end up hating the
application.  Flask provides a really simple way to give feedback to a
user with the flashing system.  The flashing system basically makes it
possible to record a message at the end of a request and access it on the next
(and only the next) request.  This is usually combined with a layout
template to expose the message.

To flash a message use the :func:`~flask.flash` method, to get hold of the
messages you can use :func:`~flask.get_flashed_messages` which is also
available in the templates. See :doc:`patterns/flashing` for a full
example.

Logging
-------

.. versionadded:: 0.3

Sometimes you might be in a situation where you deal with data that
should be correct, but actually is not.  For example you may have
some client-side code that sends an HTTP request to the server
but it's obviously malformed.  This might be caused by a user tampering
with the data, or the client code failing.  Most of the time it's okay
to reply with ``400 Bad Request`` in that situation, but sometimes
that won't do and the code has to continue working.

You may still want to log that something fishy happened.  This is where
loggers come in handy.  As of Flask 0.3 a logger is preconfigured for you
to use.

Here are some example log calls::

    app.logger.debug('A value for debugging')
    app.logger.warning('A warning occurred (%d apples)', 42)
    app.logger.error('An error occurred')

The attached :attr:`~flask.Flask.logger` is a standard logging
:class:`~logging.Logger`, so head over to the official :mod:`logging`
docs for more information.

See :doc:`errorhandling`.


Hooking in WSGI Middleware
--------------------------

To add WSGI middleware to your Flask application, wrap the application's
``wsgi_app`` attribute. For example, to apply Werkzeug's
:class:`~werkzeug.middleware.proxy_fix.ProxyFix` middleware for running
behind Nginx:

.. code-block:: python

    from werkzeug.middleware.proxy_fix import ProxyFix
    app.wsgi_app = ProxyFix(app.wsgi_app)

Wrapping ``app.wsgi_app`` instead of ``app`` means that ``app`` still
points at your Flask application, not at the middleware, so you can
continue to use and configure ``app`` directly.

Using Flask Extensions
----------------------

Extensions are packages that help you accomplish common tasks. For
example, Flask-SQLAlchemy provides SQLAlchemy support that makes it simple
and easy to use with Flask.

For more on Flask extensions, see :doc:`extensions`.

Deploying to a Web Server
-------------------------

Ready to deploy your new Flask app? See :doc:`deploying/index`.
