---
layout: page
title: About me 
---

#### About me

<footer class="post-footer">
    <!-- If we want to display author's name and bio -->
    {% if site.author %}
        <figure class="author-image">
            <a class="img" href="{{'/' | relative_url }}" style="background-image: url({{'/assets/images/profile.png' | relative_url}})">
            <span class="hidden">{{site.author}}'s Picture</span></a>
        </figure>
        <section class="author">
            <!-- Author Name -->
            <h4> {{ site.author }} </h4>
            <!-- Author Bio -->
            <p>
                There is nothing more visible than what is secret, and nothing more manifest than what is minute. Therefore the superior man is watchful over himself, when he is alone.
            </p>
        </section>
    {% endif %}
</footer>