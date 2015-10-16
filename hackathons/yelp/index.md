# Yelp

The objective of this hackathon is to design and prototype an interactive
visualization interface for exploring the Yelp dataset. Here we assume a user
in the _data exploration_ mode and may not have specific questions in mind.
Instead of answering specific questions, your interface should support
 _a class of questions_.

Some examples of _question classes_ for the Yelp dataset are:
* How many businesses are in (CITY)?
* How many businesses in the (X) categories?
* What is the distribution of businesses across categories that have
an attribute (Y)?

As you can see, each question class has a particular template with "blanks" to
fill in. Your interface should provide appropriate input fields (e.g., text,
dropdown) for users to fill in those blanks and get a different result.

## business
<pre><code>
{
    'type': 'business',
    'business_id': (encrypted business id),
    'name': (business name),
    'neighborhoods': [(hood names)],
    'full_address': (localized address),
    'city': (city),
    'state': (state),
    'latitude': latitude,
    'longitude': longitude,
    'stars': (star rating, rounded to half-stars),
    'review_count': review count,
    'categories': [(localized category names)]
    'open': True / False (corresponds to closed, not business hours),
    'hours': {
        (day_of_week): {
            'open': (HH:MM),
            'close': (HH:MM)
        },
        ...
    },
    'attributes': {
        (attribute_name): (attribute_value),
        ...
    },
}
</pre></code>
