Where did that info come from? --[Yellows8](User:Yellows8 "wikilink")
([talk](User%20talk:Yellows8.md "wikilink")) 01:29, 10 May 2018 (CDT)

A lot of fuzzing and time spent in IDA. Or are you asking for where to
look for yourself?

  -   
    So ".api\_info" / NPDM info isn't from official SDK, right?
    --[Yellows8](User:Yellows8 "wikilink")
    ([talk](User%20talk:Yellows8.md "wikilink")) 12:12, 10 May 2018
    (CDT)

<!-- end list -->

  -   
    .api\_info is found in older non-nintendo (games) applications when
    unpacked from an NSO back to an ELF. I'm not really sure what it is,
    static compilation of the SDK? Wouldn't the be stripped for
    published games? Nothing post-6 months of NX release appears to have
    it. NPDM info has been determined very lazily, a lot of modifying
    the hbmenu generated one and poking at where Horizon breaks or where
    any odd behavior happens, as well as comparison to some official
    NPDM files. If I have gotten anything wrong and someone knows
    better, well, that's what the collaborative process of a wiki is
    for. Are reversing officially released titles are fair game? If not,
    I'll remove my changes.
    --[FrasierCrane](User:FrasierCrane "wikilink")
    ([talk](User%20talk:FrasierCrane.md "wikilink")) 12:26, 10 May 2018
    (CDT)
      -   
        "Are reversing officially released titles are fair game?" Yeah
        that's fine. --[Yellows8](User:Yellows8 "wikilink")
        ([talk](User%20talk:Yellows8.md "wikilink")) 12:33, 10 May 2018
        (CDT)
