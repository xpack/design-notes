# Templates

The tools should be able to generate files.

The preferred input for the generator input is
[Shopify Liquid](https://shopify.github.io/liquid/), with tags and filters.

The context for the template engine will be the configuration object,
which includes the user xcdl objects, the xpmake objects and the
auto-discovered objects.

As comparison, Meson is able to substitute variables in autoconfig files,
like `config.h.in`.
