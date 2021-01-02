---
title: "About the relevance of changelogs of mobile apps"
date: 2021-01-02T12:00:00+01:00
draft: true
---

# About the relevance of changelogs of mobile apps

{{< table_of_contents >}}

There is an ever growing number of apps which are constantly updated.
The apps are updated due to a number of (mostly) good reasons. 
But most notably due to this reason

> Bug fixes and improvements
>
> – every app ever

We all have read that about a thousand times.
One might think that the developers would be proud to tell their users of 
their latest exciting changes. So why don't they write good changelogs?

## About changelogs

But first let's define what a changelog is and what it's intended purpose is.
[Keep a changelog](https://keepachangelog.com/en/1.0.0/#what) describes a 
changelog as

>A changelog is a file which contains a curated, chronologically ordered list of notable changes for each version of a project.

They are used to describe and inform the impact of the changes on the end user. 
Granted, frequent updates of an app reduces the amount of changes per version
and this in turn reduces the size of the impact, but nevertheless it is still 
important.

Also refer to [changelog](https://en.wikipedia.org/wiki/Changelog) and [release notes](https://en.wikipedia.org/wiki/Release_notes).

## Reasons for not writing a changelog {#noChangelog}

Well there are reasons for not writing a changelog in the app stores.
Feature toggles[^featureToggle] make it impossible to write changelogs, because
not every user already has access to it. The same applies to
[A/B-Testing](https://en.wikipedia.org/wiki/A/B_testing) in apps. Another reason
is if the developer decides to do a [canary
release](https://martinfowler.com/bliki/CanaryRelease.html)[^canaryRelease]. And
after a full introduction of feature there is no need to write it down in the
changelog because there is nothing new for the users.

Also because of the [agile software
development](https://en.wikipedia.org/wiki/Agile_software_development),
[Continuous Delivery](https://en.wikipedia.org/wiki/Continuous_delivery) and
[DevOps](https://en.wikipedia.org/wiki/DevOps) the amount of releases for apps
is growing.
[Facebook](https://research.fb.com/wp-content/uploads/2017/02/fse-rossi.pdf) for
example has written a paper about it. [This
paper](https://ieeexplore.ieee.org/document/7476674) conducted research about
which release interval are used and what developers and users are thinking about
it. So because of this growing number of releases it is getting more and more
cumbersome to write changelogs. Not to mention the localization of the
changelogs.

Okay, now I'm interested in actual numbers.


## Results 

So I've scraped 22,531 apps of the Apple App Store (because they have an API for that).

About a quarter (5,601) of those apps have a changelog which is mostly just `bug fixes and improvements`[^uselessChangelogQuery].
Also 501 apps straight up really just have `bug fixes` or `bug fixes and improvements` as a changelog[^bugFixChangelogQuery].
On the upside, three quarters of apps have a longer changelog which probably 
are a real changelogs. These types of changelog will from now on be called
'useless', because they seem mostly useless from a user perspective.

I wonder if apps with a 'useless' changelog have a better or worse average rating than apps with a better changelog.
The average rating of apps with a 'useless' changelog is about 4.031[^averageRatingOfUselessQuery], apps with a 'better' changelog have an average
rating of about 3.966[^averageRatingQuery].
The average rating of all apps is about 3.982.

The ration of paid apps with a 'useless' changelog is also higher.
I suspect this is because of the practices explained [above](#noChangelog).

|           | useless changelog |  good changelog |
|-----------|------------------:|----------------:|
| app count |              5601 |           16930 |
| free apps |              3654 |            9382 |
| paid apps |              1947 |            7548 |


## What do users think though?

So we know why developers don't provide changelogs. But what do users think 
though?

https://docs.google.com/forms/d/1Jk8e7j1gTaEHH5l95jmwUtrgUSIVW_QPN-ee6HbP6IQ/edit

## Key takeaways

What should I write then, if not a changelog?
Well, the changelog is shown more prominently after the user installed the app.
This is illustrated in the screenshots of the GitHub app page in Google Play
and the Apple App Store.

<div class="row">
    <div class="col-sm-6">
        <img src="gp_github.jpg" height="500">
    </div>
    <div class="col-sm-6">
        <img src="as_github.png" height="500">
    </div>
</div>


So this is a good place to ask for reviews, because the user is already at the
place to leave a review, or to ask the user to enable automatic updates if you
are making regular updates. Also you could use it as another place to 
advertise features in your app. But please, don't just write `Bug fixes and improvements`. Take yourself a litte time and write down something creative.
See [below](#notableMentions) for some inspiration.

You should probably create an in-app changelog dialog anyway. This is possible
with what I explained [above](#noChangelog). It also shows that your app was
updated, since automatic updates are transparent to the user. At least on Google
Play.
There are also more practical reasons why you should write a changelog.
<!-- for your own support team -->
<!-- automatic classification with user reviews through machine learning -->

## Notable mentions {#notableMentions}

There were a lot of creative changelogs. Some are listed here:

> Everything we do, we do it for you! We feel so lighthearted today – must be the weather, or the coffee we just had. Or just you. In any case we were thinking of you while we were fixing the bugs here. Have a nice day!
>
> – [ebay Kleinanzeigen](https://play.google.com/store/apps/details?id=com.ebay.kleinanzeigen&hl=en)

## Dataset

The app meta dataset is available as a SQLite database here. The queries shown above are readily available as SQL views.

The questionnaire dataset is available here.


### Thanks for reading!
Let me know what you think on [Twitter](https://twitter.com/ue_man).


## Disclaimer
This research only applies to apps in the Apple App Store and Google Play.
If you are maintaining a library, please write a changelog.

[^featureToggle]: Read about Feature Toggles [here](https://www.martinfowler.com/articles/feature-toggles.html) or [here](https://en.wikipedia.org/wiki/Feature_toggle)

[^canaryRelease]:
    The Apple App Store calls them phased releases and Google Play refers to them as [staged rollouts](https://support.google.com/googleplay/android-developer/answer/6346149?hl=en).
    The app page in both stores is always the same for everyone for a given release, except for A/B-Testing of Google Play.

[^uselessChangelogQuery]:
    <details>
    <summary>Query</summary>

    ```sql
    select title, length(releaseNotes), releaseNotes
    from AppStoreEntry
    where 
    (
        releaseNotes like '%bug%'
        or releaseNotes like '%improvements%'
        or releaseNotes like '%enhancements%'
        or releaseNotes like '%fixes%'
    )
    and length(releaseNotes) < 60
    order by length(releaseNotes) asc
    ```

    </details>

[^bugFixChangelogQuery]:
    <details>
    <summary>Query</summary>

    ```sql
    select title, length(releaseNotes), releaseNotes
    from AppStoreEntry
    where  releaseNotes like 'bug fixes and performance improvements'
    or releaseNotes like 'bug fixes and performance enhancements'
    or releaseNotes like 'bug fixes'
    or releaseNotes like 'bug fixed'
    ```
    
    </details>

[^averageRatingOfUselessQuery]:
    <details>
    <summary>Query</summary>

    ```sql
    select avg(score)
    from AppStoreEntry
    where 
    (
        releaseNotes like '%bug%'
        or releaseNotes like '%improvements%'
        or releaseNotes like '%enhancements%'
        or releaseNotes like '%fixes%'
    )
    and length(releaseNotes) < 60
    ```

    </details>

[^averageRatingQuery]:
    <details>
    <summary>Query</summary>

    ```sql
    select avg(score)
    from AppStoreEntry
    where id not in
    (
        select id
        from AppStoreEntry
        where 
        (
            releaseNotes like '%bug%'
            or releaseNotes like '%improvements%'
            or releaseNotes like '%enhancements%'
            or releaseNotes like '%fixes%'
        )
        and length(releaseNotes) < 60
    )
    ```

    </details>

