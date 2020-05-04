[](http://teacher.bmc.uu.se/BIOINFO2005/index.html)[![cri-map\"](Pictures/crimicon.gif)](index-2.html)![DataAnalysis
2](Pictures/analyse2.gif)

CRI-MAP Tutorial - Locus Insertion & Chromosomes
------------------------------------------------

------------------------------------------------------------------------

**CRI-MAP tutorial** contents:

[![Manuals](Pictures/manual.gif)](crimanua.html)

[![Manual Table of Contents](Pictures/manuatoc.gif)](manuatoc.html)

[![Data Sets](Pictures/datasets.gif)](datasets.html)

[![Data Formatting](Pictures/datafrmt.gif)](datafrmt.html)

[![Mapping & LOD scores](Pictures/analyse1.gif)](analyse1.html)

[![Bibliography & Links](Pictures/biblinks.gif)](biblinks.html)

 

[Manuals:\
Web & text\
versions](crimanua.html)

[Web Manual\
Table of\
Contents](manuatoc.html)

[ Tutorial \
 Practice \
 Datasets ](datasets.html)

[Formating\
data with\
\"`prepare`\"](datafrmt.html)

[Mapping\
with\
\"`build`\"](analyse1.html)

[Bibliography\
&\
Other Links](biblinks.html)

------------------------------------------------------------------------

6\. [Positioning a locus on a map](#all)  (`all` option)

[Ex. 6.1](#ex6.1) - locating new loci with `all`

[Ex. 6.2](#ex6.2) - checking map order with`flipsn`; reporting map
changes with `fixed`

7\. [Seeing the cross-overs](#chrompic) (`chrompic` option)

[Ex. 7.1](#ex7.1) - view the data used to produce the current map

[Ex. 7.2](#ex7.2) - evaluate the dataset used and plan itsimprovement

8\. [An Evaluation of Our Map](#conclusion)

[]{#all}

------------------------------------------------------------------------

### 6. Positioning a locus on a map

Time for a short review. So far we have assembled a \"best\" map of
27loci spanning close to 230 cM. We did this in two stages, in two
rounds of`twopoint -> build -> flips2` combinations, andincreased the
map first from three loci to twelve, and next from twelve to 27.To
achieve the first round map, we relied slightly on (and were mislead by,
onoccasion) cytological data, and avoided the mapping information stored
in the`chr2.ord` file. The reason for this was to force**CRI-MAP** to
construct its maps using the data afresh each time,without possibly
incorrect constraints on the true locus order from previous`build`
runs.\
To get the second round map, we ignored the cytological data and
usedtwopoint linkage data combined with the mapping information stored
in the`chr2.ord` file. We also relaxed the stringency for adding loci
tothe first round map.\
Now we have a large map, a high degree of confidence in *most*of it, and
a substantial database of possible locus orders for those
locistill-to-be-placed, residing in the `chr220.ord` file. Giventhat we
have just improved the current map - by reversing one pair of loci
togive a better LOD score - can the `chr220.ord` file be used to mapor
approximate the position of as-yet-unmapped loci? No, unfortunately not.
Thenew locus order doesn\'t occur in `chr220.ord`, so any**CRI-MAP**
options (e.g., `build, instant, quick`) thatuse this file to augment the
current map will reject ALL new maps!

[![](Pictures/manualsm.gif)](wwwversn.html#RTFToC35)The option of choice
for positioning one new or a couple of difficult old lociis
[`all`](wwwversn.html#RTFToC35); forthe loci in the `inserted_loci`
parametre it tests *all* possiblepositions and combinations of positions
along the current map, and reports theLOD scores. If one of the position
combinations has a LOD score at least 2.000better than any other, we can
manually insert the loci at their positions andaugment the current map.\
[Which]{#whichloci} loci from the chromosome 2 dataset are
goodcandidates for use with`all`? For \"new\" loci, there are the two
*p* arm locithat were excluded from the secondround of `build` runs
because they showed no twopoint linkage to the12 locus map:
`D2S61_2 (64) & CPSI (9)`. There are also two*q* arm loci that show
linkage to some of the recently added loci ofthe current map:
`CRYG1-5 (0) & D2S35 (14)` (data from a`twopoint` run not shown.) For
problematic old loci, there are thosethat DID enter the second round
maps of **Try 218 & Try 219**but were omitted from the \"best\" map of
**Try 220**because they could not be uniquely placed:
`D2S39 (22), D2S36 (13), &GYPC (58)`.\
Trying to position these seven loci somewhere in the 27 loci of
thecurrent map with one `all` run will NOT work. Most computers don\'t
haveenough memory to evaluate and store the \>27 x10^9^ 34 locus
mapsthis calculation calls for. On the other hand, trying only one locus
at a timecan sacrifice some analytical power, if the insertion of loci
is mutuallysupporting. For example, we know
from[`build220.out`](datasets/chr2/build220.html#gypc)that loci
`D2S39 (22), D2S36 (13), & GYPC (58)` don\'t have uniquepositions along
the current map with a LOD score stringency of 2.000 .Trying to insert
these three loci - one at a time - using `all` willsimply repeat what we
know from `build220.out` . A better strategymight be to attempt
inserting these difficult loci in pairs, or in combinationwith one of
the \"new\" loci from above. Rather than try the 21 possibletwo locus
combinations possible with these seven loci, however (the `all`option is
one of the more computationally intensive and this would take far
toolong), try each of the four new loci from the *p* & *q* arms.If one
or more of these fits uniquely, `twopoint` will reveal which ofthe
remaining loci - alone or in pairs - might next insert via `all`.

[](wwwversn.html#RTFToC35)
:   ***Exercise** CRI-MAP [6.1]{#ex6.1}: positionloci on a map -
    locating new loci with* `all`*\
    *
:   Create four new `chr22*.par` *files from*`chr222.par` *by adding one
    of* `0, 9, 14,` *or*`64` *to the* `inserted_loci` *parametre. For
    eachnew file, copy it to* `chr2.par` *and save the output
    of\"*`crimap 2 all`*\" to* `all22*.out` *.*
:   Add any locus to the current map if it meets the standard for
    inclusion,a unique position at a stringency of LOD score \>= 2.000 .
:   Create `chr227.par` *with NO loci in the*`ordered_loci` *parametre
    and the four new plus the three oldloci as the* `inserted_loci`*.
    Copy* `chr227.par`*to* `chr2.par`*, and examine the output of
    a*`twopoint` *run. If one or more of the four new loci were addedto
    the curent map in the previous step, list the loci showing linkage
    to thesefirst. Next note any locus pairs showing linkage. Starting
    at the top of thelist, choose two or three loci for further
    analysis; if you chose three loci,make three different locus pairs.
    Create the new* `chr22*.par`*file(s) from* `chr222.par`*,
    augmenting*`ordered_loci` *to reflect the current map, and adding
    the locuspair(s) to the* `inserted_loci`*. Try to insert the locus
    pair(s)using* `all`*. (**NB:** If you find and try toinsert a trio
    of loci - all three loci at once - **CRI-MAP**will run for a day or
    two! Please run any jobs like this as*`batch` *jobs!)*
:   Add any loci to the current map if they meet the standard
    forinclusion.

[]{#6.1disc}

[`all223.out`](datasets/chr2/all223.html#order) shows thatlocus
`CRYG1-5 (0)` \"fits\" uniquely into the extant map, butthe other
`all22*.out` files show two or three possible positions forthe three
other loci. These others are maximally likely only at theends of the
map, and there is almost no preference for one end over the other.We can
only use locus `CRYG1-5 (0)` to augment the current map.\
In the test for twopoint linkage among the seven trial loci, only four
locishow significant linkage
relationships([`2pt227.out`](datasets/chr2/2pt227.html#links)).Luckily,
one of these four is locus `CRYG1-5`, and it is linked
to`CPS1 (9) & D2S35 (14)`. In addition, `D2S35` shows linkageto
`D2S39 (22)`.\
Trying to insert these loci in three different pairs
(`9 14 -all228.out; 9 22 -all229.out; 14 22 -all230.out`) proves
unsuccessful,however. Perhaps first adding more *q* arm loci, via a
third round of`build` runs would help; you are welcome to do the
experiments!

With a new locus added to the current map, the remaining steps are:

1.  `flips2 & flips3` - to checkthat the new map is in the best order
    (`flips3` becausethe new locus has been added at one end), and
2.  `fixed` - to report the details of this final map.

[](wwwversn.html#RTFToC38)
:   ***Exercise** CRI-MAP [6.2]{#ex6.2}: position locion a map -
    checking the order of the new map with*`flipsn`*; reporting any
    changes to the mapwith* `fixed`*\
    *
:   Using `chr230.par` *as* `chr2.par`*, savethe outputs of
    \"*`crimap 2 flips2`*\" andas \"*`crimap 2 flips3`*\"
    as[`flip2230.out`
    *and[`flip3230.out`*,respectively.*](datasets/chr2/flip3230.html#pairrev)*](datasets/chr2/flip2230.html#pairrev)*
:   Modify the `ordered_loci` *parametre of*`chr2.par` *if necessary,
    and save the output of\"*`crimap 2 fixed`\"
    as[`fixed2.out`](datasets/chr2/fixed230.html).

The `flipsn` shows that no changes in map order arerequired! As before,
though, there are **a few locus pairreversals** that are within a LOD
score of 3.000 of[this best map](datasets/chr2/flip2230.html#pairrev).\
The final map of the *p* arm of chromosome 2 incorporates 28 loci(36
when haplotyped loci are included), spans 254.0 cM, and has a LOD
scoreof -1141.012 .

[]{#chrompic}

------------------------------------------------------------------------

### 7. Finding recombination events in the pedigrees

The map we\'ve produced has strong support for *most* of its length;in
reporting this map to colleagues, the reduced confidence we have in
theorder of 8 locus pairs could be indicated as follows:

             77          10       28       70 0 55 68  1 49 20 69 33 59 26 40 31 66 56 54 50 44 65 42 5 21 61                24             17

This *conservative* map has 20 backbone loci, plus eight others
thatprobably go just before (if above) or just after (if below) their
backboneneighbours.

[](wwwversn.html#RTFToC37)Unsatisfied with reporting a conservative map?
Another possibility is to goback to the dataset to see where its
weaknesses lie, and to do another fewexperiments that will confirm or
deny the current map.**CRI-MAP**\'s tool for viewing the data used for a
particularmap is the `chrompic` option.

:   ***Exercise** CRI-MAP [7.1]{#ex7.1}: Seeing thecross-overs - view
    the data used to produce the current map*
:   Enter the command \"`crimap 2 chrompic`*\", andsave the output
    as*[`chrpc230.out`](datasets/chr2/chrpc230.html).(**NB:** this file
    is \~100 K!)

The `chrompic` option takes from the dataset all the information usedto
produce the current map, and re-formats it for easy inspection. As with
most**CRI-MAP** options, the `chrompic` output begins with a[restatement
of the parametres](datasets/chr2/chrpc230.html#params)that were used. It
then lists map-specific data for each family in the dataset.For example,
the first family in the dataset,[Family
1326](datasets/chr2/chrpc230.html#1326),has no data relevant to the
current map. Each individual from \#3 to \#9 isshown with two lines of
36 \"dashes\" beside it, and the number`0` beside each line.

The lines represent the two copies of chromosome 2 in eachperson, the
dashes represent the loci of the current map, and the number countsthe
cross-over events estimated to have occurred on that chromosome for
theloci in their current order. There are 36 dashes because
`chrompic`also reports on the loci in haplotyped systems.

The first family with relevant information is[Family
1328](datasets/chr2/chrpc230.html#1328).

Looking atindividual \#3, both of her chromosomes have been scored for
seven of the 36loci of the current map. Her maternal chromosome (above)
has data for map loci1 7 24 26 27 28 & 29 (these are loci
`CRYG1-5 D2S44 D2S6 D2S46 D2S48APOB_2 & APOB`) and her paternal
chromosome (below) has data for maploci 7 24 26 27 29 33 & 36
(`D2S44 D2S6 D2S46 D2S48 APOB D2S47 &ACP1`). Further, individual \#3
hasone cross-over on the maternal chromosome, between map loci 1 & 7,
whichplaces six paternal (`i`) alleles for
`D2S44 D2S6 D2S46 D2S48 APOB_2& APOB` on the otherwise maternal (`o`)
chromosome. Twocross-overs on the paternal chromosomeplace maternal
alleles for `D2S6` and `D2S46`. Note the precisionwith which these
cross-over events are placed; quite precisely between maploci 26 and 27
for the second cross-over on the paternal chromosome, and withvery
little precision for the first cross-over - somewhere between map loci7
and 24. Finally, note that all data from this family isphase unknown,
indicated by the use of lower case letters (`i` and`o`) to show loci as
either paternally or maternally inherited.

[After the family data]{#infint} comes the[summary of
informativeintervals](datasets/chr2/chrpc230.html#infint). An interval,
the gap between any two loci on the current map,is *informative* if one
or more cross-overs are recorded withinit. Thus, when we look at the
\"`1____7`\" interval, we seeit holds six cross-overs, one being from
`1328-3-M` (Family 1328,individual \#3, maternal chromosome).

Finally, the `chrompic` output ends with the[identities of the
haplotypedloci](datasets/chr2/chrpc230.html#haploloci) in the current
map, and the details of the[Sex-Averaged
Map](datasets/chr2/chrpc230.html#map).

The section of `chrpc230.out` that summarizes the cross-over
chromosomesis the most useful for findingweaknesses in the dataset and
seeing ways to improve them. One set of intervalswith little support in
the current map is the set among loci
`D2S44,Prot_C/pcr, D2S54+D2S54_2, & LCO`, or, among map loci 7 through
11.(Recall that the locus order `D2S44 D2S54+D2S54_2 Prot_C/pcr LCO`has
only slightly less support than the current map,[a LOD score decrease of
0.76](datasets/chr2/flip3230.html#pairrev))Counting the cross-overs in
each interval of this set gives a rough feelingfor why.

          Locus IDs       68      77      1,3     49      Map Loci       __7_______8______9,10____11__      cross-over #     |---9---|---5---|---4---|      per interval     |------11-------|                               |-------8-------|                       |----------10-----------|

There are almost as many cross-overs in interval\"`8____11`\" (8) as
there are in total between\"`8__9,10`\" and\"`9,10__11`\" (4+5=9).
Increasing the cross-over countsin interval \"`8__9,10`\" and
\"`9,10__11`\"would strengthen the support for current map, as would
decreasing the count ininterval \"`8____11`\". A quick improvement could
come fromanalysing the families with cross-overs in interval
\"`8____11`\"for the one of the two map loci `9 & 10`
(`D2S54 &D2S54_2`). Similarly, support for the current map would improve
if therewere fewer cross-overs in the \"`7____9,10`\" interval andmore
between loci `7 & 8` and between `8 & 9,10` .Which families should be
re-analysed, and for what loci?

:   ***Exercise** CRI-MAP [7.2]{#ex7.2}: Seeing thecross-overs -
    evaluate the dataset used and plan its improvement*
:   List the families that could be re-evaluated for inheritance
    patterns toimprove the mapping of loci
    `D2S44, Prot_C/pcr, D2S54+D2S54_2, &LCO`*. Specify the loci to be
    tested in each family and rank thefamilies by likely
    informativeness.*

Below is an excerpt from `chrpc230.out` . There are 15 families
havingthe 29 cross-overs in one of the three intervals\"`7____9,10`\",
\"`7____11`\" &\"`8____11`\".

Seven of these families have only one individual with a cross-over in a
relevantinterval, and six families have only two individuals; scoring
entire families fornew loci to scrutinise one or two cross-over events
is unlikely to be anefficient use of resources.\
Two families, 1359 & 1375, have tenindividuals with relevant
cross-overs. Family 1375 is only reported inthe \"`8____11`\" interval,
and so would require further analysisonly at one locus, either `D2S54`
or `D2S54_2`. Family1359 is reported once in the \"`7____9`\" interval
andfive times in interval \"`7____11`\"; this family needs rescoringfor
loci `Prot_C/pcr & (D2S54 or D2S54_2)`. If forced to choose oneof these
two families for further analysis, I would choose[Family
1375](datasets/chr2/chrpc230.html#1375).Though it has fewer relevant
cross-overs (4 vs. 6), it also has fewerindividuals to score than 1359
(13 vs. 18), and for only one locusinstead of two. Perhaps the most
compelling reason to choose Family1375 over 1359 is that much of its
extant data is from phaseknown meioses, while Family 1359 has only phase
unknown data.

[]{#conclusion}

------------------------------------------------------------------------

### 8. An Evaluation of Our Map

A complete analysis of this dataset has been published in:\
`Spurr, N. et al 1992 The CEPH Consortium LinkageMap of Human Chromosome 2. GENOMICS 14:1055-1063`\

How does the partial map built in this tutorial compare? Here\'s our
conservativemap of the *p* arm again.

             77          10       28       70 0 55 68  1 49 20 69 33 59 26 40 31 66 56 54 50 44 65 42 5 21 61                24             17

And here\'s the 1992 CEPH Consortium map, reformatted for comparison.

                   1274 47 51 48  9  0 14 30 11 27 18 61 68  1 49 20 69 10 24 59 26 35 40 31 66 56 70 54 50 42                52 43                   16                75       15

The maps are almost identical for the order of the loci they share. The
onedifference is the locus pair `56 70`, already flagged in our map
ashaving weak support. As for the loci the maps do not share, many of
the extraloci in the consortium map are *q* arm loci we chose to ignore
(e.g.,`74 47 51 etc.`). Other extra loci close to or on *p* arm of
theconsortium map (`18 16 75 35 15`) are compensated by extra
backboneloci in our conservative map (`55 33 44 65 5`) and by the other
extraloci with weaker support (`21 77 28 17`).

I wish you good fortune with your use of **CRI-MAP**!

------------------------------------------------------------------------

[![](Pictures/embticon.gif)](http://teacher.bmc.uu.se/BIOINFO2005/index.html)[![](Pictures/hgmbicon.gif)](http://www.embnet.org/index.html)

------------------------------------------------------------------------

[**Comments? Questions? Accolades?**]{#comments}\
*Please* talk to your teacher  **( )**

------------------------------------------------------------------------

Updated on Wednesday, 22 January, 2005\
Copyright
