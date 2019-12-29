+++
date = "2017-03-17T11:29:17+01:00"
title = "PentahoNL meetup March 2017 recap"
draft = false
author = "Rogier Wessel"
tags = ["meetup", "pentaho"]
post = "/:year/:month/:day/:slug.html"
image = "images/cover.jpg"
comments = true
share = true

+++

# Great vibe, interesting talks

We had another great [PentahoNL](https://www.meetup.com/Pentaho-NL-Meetup/events/236959320/) meetup last week.

This session was hosted by [Rob Smienk](https://twitter.com/maskerade1) at the offices of  [@_MRDM_](https://twitter.com/_mrdm_) in Deventer. [@_MRDM_](https://twitter.com/_mrdm_) is a company specialized in aggregating Medical data and registration data to gather better insights in Medical processes and treatment outcomes.

Hospitals and University Medical Centers increasingly need to report and clarify on Costs and Quality of medical treatments. They gather data from connected Hospitals, aggregate and benchmark the results. They are growing fast, moving into other European markets as we speak, and are actively [seeking new keyboard cowboys](https://www.mrdm.nl/page/vacatures).

# MRDM: PDI by components
*Rob Smienk*

Metadata driven highly componentized etl as developed at MRDM. By building small components and glueing them together with a homemade orchestration framework these guys are able to quickly onboard new datasets by mix and matching suitable components. Highly agile, I was impressed and inspired by their approach.

<iframe id="iframe_container" frameborder="0" webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen="" width="700" height="510" src="https://prezi.com/embed/5kov4ml6fyre/?bgcolor=ffffff&amp;lock_to_path=0&amp;autoplay=0&amp;autohide_ctrls=0&amp;landing_data=bHVZZmNaNDBIWnNjdEVENDRhZDFNZGNIUE1iOUU4aWJ6aDNMU2VEWHN4MlNURGwvc3BCa1poUnZWSDJKcWxmNzhxcz0&amp;landing_sign=mNxxS6ytyAfMBJ75uob9akE2xSQpZi0EzJVI0sPYrvY"></iframe>

# MRDM: ETL testing
*Rutger Deterd Oude Weme*

The small components suite perfectly for TDD [(Test Driven Development)](https://en.wikipedia.org/wiki/Test-driven_development), it was the first group I have seen following up so strongly on TDD in the Pentaho "ecosphere", should be applied much more (at least I'll try to follow up on their guidelines more seriously).

<iframe id="iframe_container" frameborder="0" webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen="" width="700" height="510" src="https://prezi.com/embed/wcpw8wjmrfad/?bgcolor=ffffff&amp;lock_to_path=0&amp;autoplay=0&amp;autohide_ctrls=0&amp;landing_data=bHVZZmNaNDBIWnNjdEVENDRhZDFNZGNIUE1iOUU4aWJ6aDNMU2VEWHN4M0R5NE1adDArMHBKZFZ5eUhsWm5GT0RXcz0&amp;landing_sign=kkGb--EbKdlhnoHws1pXgwd6GVWYTg-N5CcVs3aUb4I"></iframe>

# Continuous Delivery of Etl, from git to carte in a (couple off) sec(s)
*Rogier Wessel*

[I talked but mostly demo-ed](https://github.com/blijblijblij/presentations/blob/develop/201703%20-%20pentaho%20nl%20meetup/Continuous%20Delivery%20of%20Etl%2C%20from%20git%20to%20carte%20in%20a%20(couple%20off)%20sec(s).pdf) our Continuous Delivery setup. We utilize the power of Docker, Apache Mesos with some help of a CI (Teamcity) to quickly build and deploy new ETL as it gets committed to git(hub).

# To conclude
I think the combination of talks was very complementary, from different points of the challenge of building solid ETL we showed how to make finely grained, highly testable and quickly releasable code.

Really wonder what will be next time, hope to see you guys soon!
