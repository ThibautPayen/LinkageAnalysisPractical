[](http://teacher.bmc.uu.se/BIOINFO2005/index.html)[![cri-map\"](Pictures/crimicon.gif)](index-2.html)[](analyse1.html#conceptex)[![](Pictures/analy1sm.gif)](analyse1.html#conceptex)

Typical **CRIMAP** `build` run
------------------------------

 

------------------------------------------------------------------------

In this short, conceptual example, the **CRIMAP** `build`option adds
loci `D` and `E` to an existing map of three loci,\"`A  B  C`\". The
steps are as follows:

1.  choose the most informative locus of the two, `D`,
2.  evaluate the four possible placements of locus `D` in the existing
    map,

        D  A  B  CA  D  B  CA  B  D  CA  B  C  D

    first using data from phase known meioses,

3.  discard any of these four possible maps having a likelihood score
    morethan `PK_LIKE_TOL` worse than the most likely map, thus
    retaining

        D  A  B  CA  D  B  C

4.  see that this number of possible maps is less than the maximum
    numbertolerable, `PK_NUM_ORD_TOL`, and retain them all for testing
    with thenext locus,
5.  choose the next most informative locus, `E`,
6.  evaluate the ten possible placements of locus `E` in the two
    existing maps,

        E  D  A  B  CD  E  A  B  CD  A  E  B  CD  A  B  E  CD  A  B  C  EE  A  D  B  CA  E  D  B  CA  D  E  B  CA  D  B  E  CA  D  B  C  E

    using phase known data,

7.  discard any of these ten possible maps having a likelihood score
    morethan `PK_LIKE_TOL` worse than the most likely map, thus
    retainingonly the first three of the second set of five,

        E  A  D  B  CA  E  D  B  CA  D  E  B  C

8.  see that there are no more loci to add,
9.  extract from these three maps a set of \"uniquely ordered
    loci\",\"`A  D  B  C`\",
10. evaluate the five possible placements of locus E in this map, now
    usingphase unknown data,
11. discard any of these five possible maps having a likelihood score
    morethan `PUK_LIKE_TOL` worse than the most likely map, thus
    retainingonly the first two,

        E  A  D  B  CA  E  D  B  C

12. see that there are no more loci to add,
13. extract from these two maps the set of \"uniquely ordered
    loci\",\"`A  D  B  C`\", and finally
14. report this map with interlocus distances, and report the two
    possiblepositions of locus `E`, together with the likelihood of
    each.

------------------------------------------------------------------------
