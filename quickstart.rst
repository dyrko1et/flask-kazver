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

Көрсету үлгілері
-------------------

Python-дан HTML жасау қызық емес және іс жүзінде өте қиын, өйткені қолданбаның қауіпсіздігін қамтамасыз ету үшін HTML-ді өзіңіз қорғауыңыз керек. Сол үшін Flask  -  `Jinja2 <https://pallets projects.com/p/jinja/>` -  шаблон қозғалтқышы автоматты түрде орнатады

Үлгілерді кез келген түрдегі мәтіндік файл жасау үшін пайдалануға болады. Веб-қосымшалар үшін Сіз бірінші кезекте HTML беттерін жасайсыз, бірақ сіз markdown, электрондық пошталарға арналған қарапайым мәтін және басқаларын жасай аласыз.

HTML, CSS және басқа веб-API-ге сілтеме жасау үшін 'MDN Web Docs'_.

.. _MDN Web Docs: https://developer.mozilla.org/

Үлгіні көрсету үшін :func:`~flask.render_template` әдісті қолдануға болады . Сізге тек шаблон атауын және шаблон қозғалтқышына кілт сөз аргументтері ретінде бергіңіз келетін айнымалыларды көрсету керек. Міне, үлгіні қалай салу керектігінің қарапайым мысалы::

    from flask import render_template

    @app.route('/hello/')
    @app.route('/hello/<name>')
    def hello(name=None):
        return render_template('hello.html', name=name)

Flask үлгілерді :file:`templates ' қалтасынан іздейді. Сонымен, егер сіздің қосымшаңыз модуль болса, онда бұл қалта сол модульдің қасында, егер ол пакет болса, онда ол сіздің пакетіңіздің ішінде болады:

**Кейс 1**: a module::

    /application.py
    /templates
        /hello.html

**Кейс 2**: a package::

    /application
        /__init__.py
        /templates
            /hello.html

Шаблондар жасау үшін Сіз Jinja2 шаблондарының барлық күшін пайдалана аласыз. Jinja2 үлгісі бойынша ресми құжаттаманы <https://jinja.palletsprojects.com/templates / > ' _  қосымша ақпарат алу үшін.

Міне мысал үлгісі:

.. sourcecode:: html+jinja

    <!doctype html>
    <title>Hello from Flask</title>
    {% if name %}
      <h1>Hello {{ name }}!</h1>
    {% else %}
      <h1>Hello, World!</h1>
    {% endif %}

Үлгілердің ішінде сізге :data:`~flask.Flask.config`, :class:`~flask.request`, :class:`~flask.session` және :class:`~flask.g` [#]_ қол жетімді нысандар , сондай-ақ пен мүмкіндіктер:  :func:`~flask.url_for` және :func:`~flask.get_flashed_messages`

Үлгілер, егер мұрагерлік қолданылса, әсіресе пайдалы. Егер сіз оның қалай жұмыс істейтінін білгіңіз келсе, қараңыз :doc:`patterns/template inheritance`. Негізінде, шаблондардың мұрагері әр бетте белгілі бір элементтерді сақтауға мүмкіндік береді (мысалы, үстіңгі деректеме, Навигация және төменгі деректеме).

Автоматты экрандау қосулы, сондықтан ``name`` HTML болса, ол автоматты түрде қорғалады. Егер сіз айнымалыға сене алсаңыз және оның қауіпсіз HTML болатынын білсеңіз (мысалы, ол Уики белгілеуді HTML-ге түрлендіретін модульден алынғандықтан), оны қауіпсіз деп белгілеуге болады :class:`~markupsafe.Markup`  немесе ``|safe``  сүзгісін қолдану арқылы белгілеу класы. Қосымша мысалдар алу үшін Jinja2 құжаттамасын қараңыз.

Міне, қалай жұмыс істейтіні туралы қысқаша кіріспе :class:`~markupsafe.Markup`.Белгілеу класы жұмыс істейді::

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

.. [#] Бұл нысанның не екенін білмейсіз  :class:`~flask.g`? Бұл ақпаратты өз қажеттіліктеріңіз үшін сақтауға болатын нәрсе. Құжаттаманы қараңыз: сынып:class:`flask.g` and :doc:`patterns/sqlite3`.


Сұрау деректеріне қол жеткізу
----------------------

Веб-қосымшалар үшін клиент серверге жіберетін деректерге жауап беру өте маңызды. Flask - те бұл ақпаратты global :class:`~flask.request` нысанмен ұсынылған . Егер сізде Python тәжірибесі болса, Сіз бұл нысанның қалай жаһандық болуы және Flask қалай қауіпсіз қала алады деген сұрақтар туындауы мүмкін. Жауап жергілікті тұрғындардың контекстінде:


.. _context-locals:

Context Locals
``````````````

.. admonition:: Insider Information

  Егер сіз оның қалай жұмыс істейтінін және жергілікті контексттермен тестілерді қалай жүзеге асыруға болатындығын түсінгіңіз келсе, осы бөлімді оқып шығыңыз, әйтпесе оны өткізіп жіберіңіз.

Flask-Тегі кейбір нысандар жаһандық нысандар болып табылады, бірақ әдеттегі түрі емес. Бұл нысандар іс жүзінде белгілі бір контекст үшін жергілікті объектілерге арналған прокси-серверлер болып табылады.  Қандай толық ауыз.  Бірақ оны түсіну өте оңай.

Контекст өңдеу ағыны деп елестетіп көріңіз. Сұраныс келіп веб-сервер Жаңа ағын құруды шешеді (немесе басқа нәрсе, негізгі объект ағындардан басқа параллелизм жүйелерімен жұмыс істей алады). Flash ішкі сұраныстарды өңдеуді іске қосқанда, ол ағымдағы ағынның белсенді контекст екенін анықтайды және ағымдағы қолданба мен wsgi орталарын осы контекстке (ағынға) байланыстырады. Ол бұл түрде жасайды, сол бір қолданба басқа қолданбаны ақаусыз шақыра алады.

Сонымен, бұл сіз үшін нені білдіреді? Негізінде, егер сіз модульдік тестілеу сияқты нәрсені жасамасаңыз, бұл жағдайды мүлдем елемеуге болады. Сұрау нысанына тәуелді код кенеттен үзілетінін екенін байқа-аласыз , себебі сұрау нысаны жоқ. Шешім: сұрау нысанын өздігінен құру және оны контекстке байланыстыру. Модульдік тестілеудің ең оңай шешімі :meth:`~flask.Flask.test_request_context` . ``with`` операторымен бірге ол сынақ сұрауын байланыстырады, осылайша сіз онымен әрекеттесе аласыз. Міне мысал:: 

    from flask import request

    with app.test_request_context('/hello', method='POST'):
        # now you can do something with the request until the
        # end of the with block, such as basic assertions:
        assert request.path == '/hello'
        assert request.method == 'POST'

Тағы бір мүмкіндік бүкіл wsgi ортасын беру
:meth:`~flask.Flask.request_context` method::

    with app.request_context(environ):
        assert request.method == 'POST'

Сұрау нысаны
``````````````````

Сұрау нысаны API бөлімінде құжатталған және біз оны мұнда егжей-тегжейлі қарастырмаймыз (:class:`~flask.Request`). Міне, кейбір кең таралған операцияларға жалпы шолу. Ең алдымен, оны ``flask`` модулінен импорттау керек::

    from flask import request

Ағымдағы сұрау әдісі :attr:`~flask.Request.method`. Пішін деректеріне қол жеткізу үшін 
(``POST``немесе ``PUT``сұрауында берілген деректер)  :attr:`~flask.Request.form` атрибутты пайдалануға болады . Жоғарыда аталған екі атрибуттың толық мысалы::

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

Егер кілт ``form`` атрибутында болмаса не болады? Бұл жағдайда арнайы :exc:`KeyError`пайда болады. Сіз оны стандартты ретінде ұстай аласыз :exc:`KeyError`, бірақ олай етпесеңіз, оның орнына қате HTTP 400 сұрауының қате беті көрсетіледі. Осылайша, көптеген жағдайларда сіз бұл мәселеге тап болмайсыз.

URL (``?key=value``)  мекенжайында көрсетілген параметрлерге қол жеткізу үшін, сіз :attr:`~flask.Request.args` attribute:: пайдалана аласыз

    searchword = request.args.get('key', '')

Біз URL параметрлеріне `get`  арқылы немесе  :exc:`KeyError` арқылы ұстап алып қол жеткізуді ұсынамыз , өйткені пайдаланушылар URL мекенжайын өзгерте алады, бұл жағдайда оларға 400 қате сұрауы бар бетті ұсыну пайдаланушыға ыңғайлы болмайды.

Request объектісінің әдістері мен атрибуттарының толық тізімін алу үшін  :class:`~flask.Request` құжаттамаға өтіңіз  .


Download files
````````````

Жүктелген файлдарды Flask көмегімен оңай өңдеуге болады. HTML формасында  ``enctype="multipart/form-data"`` атрибутын орнатуды ұмытпаңыз, әйтпесе браузер сіздің файлдарыңызды мүлдем жібермейді.

Жүктелген файлдар жадта немесе файлдық жүйенің уақытша орналасуында сақталады. Бұл файлдарға :attr:`~flask.request.files` жерден қарап, сұрау обьектердін атрибутқа кіруге болады . Жүктелген әрбір файл осы сөздікте сақталады.  Ол стандартты Python :class:`file` нысаны сияқты әрекет етеді, бірақ сонымен бірге :meth:`~werkzeug.datastructures.FileStorage.save`.Бұл файлды сервер файлдық жүйесінде сақтауға мүмкіндік беретін әдіс. Міне, оның қалай жұмыс істейтінін көрсететін қарапайым мысал::

    from flask import request

    @app.route('/upload', methods=['GET', 'POST'])
    def upload_file():
        if request.method == 'POST':
            f = request.files['the_file']
            f.save('/var/www/uploads/uploaded_file.txt')
        ...

Егер сіз файл сіздің қосымшаңызға жүктелмес бұрын клиентте қалай аталғанын білгіңіз келсе, оған қол жеткізе аласыз :attr:`~werkzeug.datastructures.FileStorage.filename`  атрибуты. Дегенмен, бұл мән жалған болуы мүмкін екенін есте сақтаңыз, сондықтан бұл мәнге ешқашан сенбеңіз. Файлды серверде сақтау үшін клиент файлының атын пайдаланғыңыз келсе, оны :func:`~werkzeug.utils.secure_filename` функция арқылы жіберіңіз ::

    from werkzeug.utils import secure_filename

    @app.route('/upload', methods=['GET', 'POST'])
    def upload_file():
        if request.method == 'POST':
            file = request.files['the_file']
            file.save(f"/var/www/uploads/{secure_filename(file.filename)}")
        ...

Толығырақ мысалдар алу үшін қараңыз: :doc:`patterns/fileuploads`.

Кукилар
```````

Cookie файлдарына қол жеткізу үшін :attr:`~flask.Response.set_cookie` атрибутын қолданыз. Cookies орнату үшін :attr:`~flask.Response.set_cookie`жауап обьектердін әдістерін қолдануға болады. Клиент жіберетін барлық cookie файлдармен сөздік жауап обьектердін :attr:`~flask.Request.cookies` атрибут. Егер сіз сеанстарды пайдаланғыңыз келсе, cookie файлдарын тікелей пайдаланбаңыз, оның орнына Flask ішіндегі :ref:`sessions` пайдаланыңыз, бұл сізге cookie файлдарының үстіне қауіпсіздік қосады.

Кукиларды оқу::

    from flask import request

    @app.route('/')
    def index():
        username = request.cookies.get('username')
        # use cookies.get(key) instead of cookies[key] to not get a
        # KeyError if the cookie is missing.

Кукиларды сақтау::

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
