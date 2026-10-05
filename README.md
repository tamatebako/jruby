# tamatebako/tebako-runtime-jruby — the JRuby runtime feedstock

Repack feedstock (no compilation): the JRuby dist is a **universal** tarball
(bytecode + ruby home; `lib/jni/` ships every platform's jffi stub — see
`Tebakofile`'s probe record), so ONE env image serves all triplets; the
triplet binding comes from the composed **java owner** pair
(tamatebako/tebako-runtime-openjdk — `DEPENDS java >= 21`, spec 33's `on_runtime` form).

- Spec: [docs/spec/33](https://github.com/tamatebako/tebako/blob/main/docs/spec/33-runtime-on-runtime.md)
  (runtime-on-runtime); the jvm-mode machinery mirrors
  tamatebako/tebako-runtime-truffleruby's `flavors.jvm`.
- Owner line floor: **2.5.0** ([tamatebako/tebako#552](https://github.com/tamatebako/tebako/pull/552)
  — a pre-2.5.0 owner misroutes the composed entry).

The pair's artifact names carry the language segment
([tebako#716](https://github.com/tamatebako/tebako/issues/716)): new
publishes spell `tebako-runtime-<tebako-line>-jruby-<version>-<platform>`
(the exe per triplet) and `tebako-runtime-<tebako-line>-jruby-<version>-universal.tfs`
(the one env image), where `jruby` is this runtime's distribution
identity — an implementation of the ruby engine. Releases already
published keep the segment-less spelling forever: they are immutable and
sha256-pinned in this registry, and re-running an old tag composes that
ref's own names, self-consistently. The fetched **owner** pair's name
follows the pinned owner release's own era — `Tebakofile`'s
`owner_smoke` block gains an `implementation` key when its pin moves to
a release whose assets carry the segment.
