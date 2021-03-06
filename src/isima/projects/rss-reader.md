The RSS Reader
==============

**RSS** stands for **R**ich **S**ite **S**ummary. It is [a format for
delivering regularly changing web content](http://www.whatisrss.com/). Many
news-related sites, blogs and other online publishers syndicate their content
as an RSS Feed to whoever wants it. We usually call **RSS** all kind of [web
feeds](https://en.wikipedia.org/wiki/RSS), including both RSS and
[Atom](https://en.wikipedia.org/wiki/Atom_%28standard%29).

### RSS

RSS files are essentially XML formatted plain text:

``` xml
<!-- https://en.wikipedia.org/wiki/RSS -->
<?xml version="1.0" encoding="UTF-8" ?>
<rss version="2.0">
<channel>
    <title>RSS Title</title>
    <description>This is an example of an RSS feed</description>
    <link>http://www.example.com/main.html</link>
    <lastBuildDate>Mon, 06 Sep 2010 00:01:00 +0000 </lastBuildDate>
    <pubDate>Sun, 06 Sep 2009 16:20:00 +0000</pubDate>

    <item>
        <title>Example entry</title>
        <description>Here is some text containing an interesting description.</description>
        <link>http://www.example.com/blog/post/1</link>
        <guid isPermaLink="false">7bd204c6-1655-4c27-aeee-53f933c5395f</guid>
        <pubDate>Sun, 06 Sep 2009 16:20:00 +0000</pubDate>
    </item>
</channel>
</rss>
```

### Atom

Atom files are slightly different, but still XML documents:

```xml
<!-- https://en.wikipedia.org/wiki/Atom_%28standard%29 -->
<?xml version="1.0" encoding="utf-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
    <title>Example Feed</title>
    <subtitle>A subtitle.</subtitle>
    <link href="http://example.org/feed/" rel="self" />
    <link href="http://example.org/" />
    <id>urn:uuid:60a76c80-d399-11d9-b91C-0003939e0af6</id>
    <updated>2003-12-13T18:30:02Z</updated>

    <entry>
        <title>Atom-Powered Robots Run Amok</title>
        <link href="http://example.org/2003/12/13/atom03" />
        <link rel="alternate" type="text/html" href="http://example.org/2003/12/13/atom03.html"/>
        <link rel="edit" href="http://example.org/2003/12/13/atom03/edit"/>
        <id>urn:uuid:1225c695-cfb8-4ebb-aaaa-80da344efa6a</id>
        <updated>2003-12-13T18:30:02Z</updated>
        <summary>Some text.</summary>
        <content type="xhtml">
            <div xmlns="http://www.w3.org/1999/xhtml">
                <p>This is the entry content.</p>
            </div>
        </content>
        <author>
            <name>John Doe</name>
            <email>johndoe@example.com</email>
        </author>
    </entry>
</feed>
```

### The Reader

Generally speaking, an RSS/Atom document is called a **feed**. It contains
various metadata (`title`, `description`, etc.). A **feed** contains a set of
**entries** or **items**, depending on the format. Let's use **item** here to
make things easier. An **item** contains a set of properties such as: _title_,
_link_ and a _publication date_ (this list is not exhaustive).

An RSS Reader is a web application that is able to:

1. Subscribe to any web feed, no matter its underlying format (Atom or RSS)
2. Regularly walk through all registered web feeds and fetch new items
   (should be put in a persistent storage)
3. Display new items, ordered by date (last items first)
4. Manage registred web feeds
5. Optionally, allow to mark an item as _read_
6. Optionally, allow to organize feeds by categories (or tags)

Examples of such applications are: [Feedly](https://feedly.com), [Tiny Tiny
RSS](http://tt-rss.org/redmine/projects/tt-rss/wiki), or [digg
reader](https://digg.com/reader).

Note that fetching registered web feeds is not done by the web application, but
using a **worker**. The [Symfony Console
Component](http://symfony.com/doc/current/components/console/introduction.html)
may help you.


What You Have To Do Now
-----------------------

Write an RSS Reader.

You can use whatever tool you want as far as you can explain your choices. You
MUST write the application in PHP. For instance, you can use
[Slim](http://www.slimframework.com/), or [Silex](http://silex.sensiolabs.org/)
as framework.

Rely on [Composer](https://getcomposer.org/) and
[Packagist](https://packagist.org) to install packages, and manage your
project's dependencies. You can ask for advices regarding the libraries you
would like to use.

Your code SHOULD be versioned. I don't mind if you loose your work before the
deadline ;-)

You MUST use the Coding Standards as described in
[PSR-1](http://www.php-fig.org/psr/psr-1/) and
[PSR-2](http://www.php-fig.org/psr/psr-2/). The [PHP Coding Standards
Fixer](http://cs.sensiolabs.org/) could help you.

### The Model

**Important:** you MUST focus on the Model layer, and you MUST write this layer
yourself. No existing ORM allowed here. You MUST implement database design
patterns seen in class, but choose them carefully according to what you need to
do.

You can use a simple file as persistence storage, in YAML or JSON for instance.

If you want to use PDO, choose SQLite as database engine if you are running
your code on `etud`, otherwise feel free to use another database engine such as
PostgreSQL or MySQL.

Then again, be sure to be able to explain your choices.

### REST API

You application MUST expose a REST API through the exact same methods in your
controllers. Use the appropriate HTTP verbs (methods), and status codes.

For instance, it should be interesting to:

1. get all items through the API
2. subscribe to a feed through the API

### Testing

Software testing is a **requirement** for all developers. Your job is **not** to
write code, it is all about providing solutions for given problems. The right
solution is always the one that works.

The question is: how do you ensure that your solution works? You cannot rely on
the well-known _it works on my machine™_. This is just silly. What you need to
do is to provide a set of automated tests.

Tests are more than just _assertions_ on some properties of your application,
it is also the best documentation you can provide to your customers/users because
tests are always up to date.

So, your application MUST be tested. Write unit tests, but also functional
tests. [Behat](http://docs.behat.org/) can help you with your functional tests.
It takes sort of user stories as input ;-)

Don't expect to have more than _10/20_ if you don't provide tests!

### Presentation Layer

While it is not the goal of this project, things that look nice are always
better than ugly things, even if those things don't work. In oher words, don't
neglect the presentation/design.

### Hints

#### Content Negotiation

Content Negotiation is part of the HTTP protocol, used to serve a resource in
the best format for a client. You can read [RFC 2616:
HTTP/1.1](http://pretty-rfc.herokuapp.com/RFC2616) and [RFC 2295: content
negotiation](http://pretty-rfc.herokuapp.com/RFC2295) if you want more
information.

Content negotiation means that a single resource can be presented in different
ways, depending on the client preferences. To achieve this goal, **HTTP
headers** (`Accept`, `Accept-*`) are used by a client to tell the server about
its preferences.

Your application SHOULD be able to serve resources in:

* `HTML` using a template;
* `JSON` encoded data.

[Negotiation](https://github.com/willdurand/negotiation) can help you get the
best format from headers by handling content negotiation. The `Accept` header
**could** be found in `$_SERVER['HTTP_ACCEPT']`. It is possible to use
Negotiation with both [Silex](https://github.com/willdurand/StackNegotiation)
and [Slim](https://github.com/codeguy/Slim-Middleware).

Your implementation SHOULD accept parameters encoded in:

* `application/x-www-form-urlencoded` - used when you submit a HTML form;
* `application/json`.

When a request has a body, it should provide a `Content-Type`. This content
type header is available in either `$_SERVER['HTTP_CONTENT_TYPE']` **or**
`$_SERVER['CONTENT_TYPE']`.

#### Serialization

HTML rendering is achieved through your template engine. Rendering your data in
other formats is called _serialization_. Serialization is the process of
converting a data structure or object state into a format that can be stored.

The serialization is handled by a Serializer. This serializer can be as simple
as the `json_encode()` function or you can use the [Serializer
Component](http://symfony.com/doc/current/components/serializer.html).


Important
---------

Le projet est à rendre au plus tard le **29 Mars 2015 à 23h59 CET**. Vous ne
pouvez pas être plus de trois étudiant(e)s sur un projet.

Les formats acceptés sont :

* une archive (`tar`, `tgz` ou `zip`) ;
* **ou** un dépôt distant (`git`, `svn`, etc.).

Le projet doit être accompagné d'instructions de mise en route. Ainsi que d'un
bilan rapide de ce qui a été fait/pas fait. Le format pour ce fichier doit être
**textuel**, donc `txt` ou `markdown`. Je ne peux pas ouvrir les fichiers Word
ou Open Office.

Ce bilan n'est pas un compte rendu formel, vous pouvez simplement énumérer ce
qui a été fait et ce qui n'a pas été fait, en faisant des phrases courtes, **en
français**. Il devrait tenir sur une page, et c'est un fichier **obligatoire**.

Aucun retard ou problème technique ne sera toléré, c'est pourquoi il est
fortement conseillé de mettre également à disposition un lien de téléchargement
direct sur un service en ligne (Dropbox, Ubuntu One, Google Drive, etc.).

Si votre archive est corrompue, vous serez défaillant, faites en sorte
d'envoyer quelque chose de correct. Nous vérifierons ce point à chaque
réception d'un projet. Si votre archive est corrompue, nous vous l'indiquerons
et vous aurez avant 23h59 pour renvoyer une archive valide.

Vous devez nommer l'archive comme suit : `projet_<nom 1>_<nom 2>.zip`. Le mail
doit comporter la mention `[ZZ3F2 PHP]` dans le sujet du mail.
