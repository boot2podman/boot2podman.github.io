To replace `podman-machine` (and even Vagrant too),<br />
look no further than **Lima**: <https://lima-vm.io>

The context of this web site is mostly historical,<br />
and the projects have been deprecated/discontinued...

For Containers, see <https://floelinux.github.io><br />
(a custom OS distribution based on Tiny Core Linux)

For Kubernetes, see <https://kutter-os.github.io><br />
(a custom OS distribution based on Buildroot system)

## Posts

<ul>
{% for post in site.posts %}
  {% assign currentdate = post.date | date: "%Y" %}
  {% if currentdate != date %}
    {% unless forloop.first %}</ul>{% endunless %}
    <h3 id="y{{post.date | date: "%Y"}}">{{ currentdate }}</h3>
    <ul>
    {% assign date = currentdate %}
  {% endif %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% if forloop.last %}</ul>{% endif %}
{% endfor %}
</ul>

----
[https://github.com/boot2podman/boot2podman](https://github.com/boot2podman/boot2podman)

[https://github.com/boot2podman/machine](https://github.com/boot2podman/machine)

<div style="font-size:75%">Icon made by <a href="https://www.freepik.com/" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div>
