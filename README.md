# Firebox (working title)

A shell script to make Firefox emulate app browsers like [Ferdi](https://github.com/getferdi/ferdi) or [Rambox](https://rambox.app).

## TODOs

* Use firefox bookmarks instead of just regular strings.
  + Get all bookmarks from `places.sqlite`: `sqlite3 places.sqlite "select a.title,b.url from moz_bookmarks as a join moz_places as b on a.fk=b.id;"`
