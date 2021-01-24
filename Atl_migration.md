Core Atlanta area population actually shrinking
================
Nick Thieme
1/30/2020

By 2018, despite the longest period of economic expansion in U.S.
history, more people were leaving metro Atlanta for other parts of the
U.S. than coming into it. Contrary to claims of unfettered population
growth in Atlanta, AJC analysis of migration rates in the five-county
Atlanta region — Cobb, Clayton, DeKalb, Fulton and Gwinnett — shows that
only international migration, people moving into the Atlanta from
abroad, supported Atlanta’s adult population growth. With Covid
inhibiting the possibility and desire for international travel, that
migration will almost certainly decrease.

The five counties in the exurbs, however—Cherokee County, Douglas
County, Fayette County, Henry County, and Rockdale County— are still
attracting domestic migrants. 80% of the population growth in those
counties, 11,000 people, was due to migration, with nearly all of it
domestic. Less than half of the core’s growth is from migration.

``` r
core<-D_PEP_2 %>% mutate(intlmig = as.numeric(intlmig)) %>% 
  pivot_longer(-c("name", "year"), names_to="type", values_to="migration") %>% 
  filter(name%in%c("Fulton County, Georgia", "DeKalb County, Georgia", 
                   "Cobb County, Georgia",
                   "Gwinnett County, Georgia","Clayton County, Georgia"))%>% 
  group_by(year, type) %>% summarise( net_flow = sum(as.numeric(migration))) %>% 
  ggplot(aes(x = year, y = net_flow,fill = type))+
  geom_smooth(aes(color = type),se=FALSE)+
  geom_point(shape =21, color = "black", size =1)+
  scale_color_viridis(discrete = T,option ="plasma", 
                      labels = c("Domestic", "International","Total"))+
  scale_fill_viridis(discrete = T,option ="plasma", 
                      labels = c("Domestic", "International","Total"))+
  ylab("Migration")+ggtitle("")+ylim(-10000,60000)+
  bbc_style()

ex<-D_PEP_2 %>% mutate(intlmig = as.numeric(intlmig)) %>%
  pivot_longer(-c("name", "year"), names_to="type", values_to="migration") %>% 
  filter(name%in%c("Cherokee County, Georgia", "Douglas County, Georgia", "Fayette County, Georgia",
                   "Henry County, Georgia","Rockdale County, Georgia"))%>% 
  group_by(year, type) %>% summarise( net_flow = sum(as.numeric(migration))) %>%
 ggplot(aes(x = year, y = net_flow,fill = type))+
  geom_smooth(aes(color = type),se=FALSE)+
  geom_point(shape =21, color = "black", size =1)+ theme_minimal()+
  scale_color_viridis(discrete = T,option ="plasma")+
  scale_fill_viridis(discrete = T,option ="plasma")+
  ylim(-10000,60000)+ylab("Migration")+
  bbc_style()

plt<-ggarrange(core, ex, common.legend = TRUE, align="h")

plt<-addSmallLegend(plt)

annotate_figure(plt,top = text_grob("Core and Exurbs", size = 16, 
                                  face = "bold"))
```

![](Atl_migration_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

Mike Carnathan, manager of the Atlanta Regional Council’s (ARC) Research
and Analytics Division, has viewed the AJC’s analysis, and agrees with
our findings. According to him, “affordable housing (is) my number one
culprit. It’s just getting harder and harder to find affordable homes in
the right type of unit and housing in our core counties.”

## Aren’t “We full”?

The AJC’s analysis flies in the face of the usual story of unfettered
population growth in Atlanta, and the ARC was originally surprised when
presented with these results. How is Atlanta actually losing local
residents when all we hear is that it’s growing?

It all comes down to how we define Atlanta. The definitions of which
areas make up Atlanta have masked significant population changes in the
core city.

In 2018, Atlanta had the 4th fastest growing population of any metro
area in the country, that’s true. There were 75,000 more people in
“Metro Atlanta” in 2018 than in 2017. But the Census, which provides
those numbers, counts 29 counties as being in “Metro Atlanta,” including
three that border Alabama, one that overlaps with the
Chattahoochee-Oconee National Forest at the state’s northern border, and
Locust Grove, GA—population 5,500, described by Georgia’s official
tourism website as “along I-75 comfortably south of Atlanta”

For the Census Bureau, which defines metropolitan statistical areas
(“metros”) based on who commutes where, those 29 counties make sense,
but if someone’s curious how much the colloquial Atlanta has grown, it
doesn’t.

The Atlanta Regional Commission, Atlanta’s regional planning agency,
also has a definition of Atlanta, and using their set of counties,
“Atlanta” grew by about 50,000 people last year. But while their
definition only includes 10 counties, the problem is the same.

Only two of those counties—Fulton County and DeKalb County—contain the
City of Atlanta, and only five of them—Fulton County, DeKalb County,
Cobb County, Clayton County, and Gwinnett County—are generally
considered core Atlanta counties.

In order to discover this, the AJC analyzed and compared three separate
sources of population data to ensure the population surprise wasn’t a
peculiarity of a single agency’s way of counting. We analyzed tax
filings from the Internal Revenue Service, population counts from the
Census Bureau’s Population Estimates Program, and population counts from
the Census Bureau’s American Community Survey. While there were slight
variations between all three, the high-level conclusions (that Atlanta’s
migration growth is driven by international migration, and that more
people are moving out of Atlanta than into it) held for all three
sources.

## Lasting effects of the Great Recession

Atlanta isn’t unique in this regard, though its demographic changes are
especially stark. Immigration is driving urban growth around the
country. The Pew Research Center estimates that without future
immigrants, the working-age population of the U.S. would decrease
between 2017 and 2035. Including immigrants in the calculation, they
estimate an increase of 10 million workers.

Those immigrants are supporting both our economy and our culture. Lyman
Stone, an economist and demographer at the United States Department of
Agriculture“ told the AJC that “losing people is losing.“ “Your
society…is impoverished, not even necessarily literally, but
culturally, socially, and morally impoverished because the unique
contributions of another person are not going to occur.”

The economic effects aren’t much better. Areas with negative population
growth “have less entrepreneurship, less patenting, less business
formation, have lost manufacturing industries faster (than areas with
positive growth), they experience greater capture of corporate profits
among managers rather than workers, they experience more inequality.
There’s this whole cavalcade of horrors.”

If it wasn’t for immigrants, the Metro area would have lost about 6,000
people to migration last year—instead, it gained 9,000. As a whole, the
core counties are experiencing domestic out-migration. Only
international migration and births are supporting population growth.

On the other hand, the five counties in the exurbs—Cherokee County,
Douglas County, Fayette County, Henry County, and Rockdale County— are
still filling up because of domestic migration. 80% of the population
growth in those counties, 11,000 people, was due to migration, with
nearly all of it domestic. Less than half of the core’s growth is from
migration.

And, unlike the core, domestic migration to the exurbs is still
increasing.

Amazingly, Atlanta’s out-migration isn’t new. It’s the continuation of a
trend that started in 2007 with the Great Recession. As the economy fell
from the sky on the burnt wings of faulty financial products and bad
housing debt, net domestic migration into Atlanta’s core fell from
30,000 people to a minimum of about 0 in 2009. Carnathan described the
2000’s as “essentially a lost decade.”

Migration stabilized after the recession, increasing to about 10,000
people per year until about 2016, when it started nosediving—hitting 0
again in 2017, and becoming negative in the most recent data.

International migration has been much more stable. While it’s still
decreased, from 25,000 in 2006 to about 15,000 in 2018, it never
suffered the collapse of domestic migration in response to the
recession.

Despite these demographic changes, Atlanta is still seeing an increasing
number of jobs–seemingly a contradiction. Part of the explanation for
how a city like Atlanta can have negative net domestic migration is that
the families leaving Atlanta have more kids than the families coming in.
If one family with three kids is replaced by two single 20-somethings,
there’s a net migration of negative three.

That trading of larger families for smaller one has occurred every year
for the last 15 years in every core county but Gwinnett County and
Clayton County in 2014. Gwinnett, the most international of the core
counties, has seen larger families move in for each of the last 15
years.

The exact opposite is true in the exurbs. For each of the last 15 years,
the average family size for families moving the exurbs from elsewhere in
the U.S. has been larger than the average family size of those leaving.

``` r
# 
# core_inc<-D_IRS_06_18 %>% filter(state==13) %>% 
#   filter(name%in%c( "Cobb County", "Clayton County", "DeKalb County","Fulton County", "Gwinnett County",  
#                    "Dekalb County", "De Kalb County")) %>% 
#   mutate(name = case_when(name%in%c("DeKalb County", "Dekalb County", "De Kalb County")~"DeKalb County", 
#                           name%in%c("DeKalb County", "Dekalb County", "De Kalb County")==FALSE~name)) %>%
#   mutate(avg_ex_p_r_in = exempts_in/returns_in,avg_ex_p_ret_out = exempts_out/returns_out, 
#          diff_in_avg = avg_ex_p_r_in-avg_ex_p_ret_out, avg_agi_in = agi_in/exempts_in, 
#          avg_agi_out = agi_out/exempts_out, avg_agi_diff = avg_agi_in-avg_agi_out) %>%
#   select(name, year, returns.d, exempts.d, agi.d, avg_ex_p_r_in, avg_ex_p_ret_out, diff_in_avg,
#          avg_agi_in,avg_agi_out,avg_agi_diff)%>%
#   ggplot(aes(x = year, y = avg_agi_diff, fill = name))+
#   geom_smooth(aes(color = name),se=FALSE)+
#   #geom_point(shape =21, color = "black", size =2)+
#   scale_color_brewer(palette = "Paired", name="County")+
#   scale_fill_brewer(palette = "Paired", name="County")+
#   geom_hline(yintercept = 0)+
#   xlab("year")+ylab("Change in 'average gross income'")+
#   bbc_style()
# 
# core_inc<-addSmallLegend(core_inc)
# 
# ex_inc<-D_IRS_06_18 %>% filter(state==13) %>% 
#   filter(name%in%c( "Cherokee County","Douglas County", "Fayette County","Henry County","Rockdale County")) %>%
#   mutate(avg_ex_p_r_in = exempts_in/returns_in,avg_ex_p_ret_out = exempts_out/returns_out, 
#          diff_in_avg = avg_ex_p_r_in-avg_ex_p_ret_out, avg_agi_in = agi_in/exempts_in, 
#          avg_agi_out = agi_out/exempts_out, avg_agi_diff = avg_agi_in-avg_agi_out) %>%
#   select(name, year, returns.d, exempts.d, agi.d, avg_ex_p_r_in, avg_ex_p_ret_out, diff_in_avg,
#          avg_agi_in,avg_agi_out,avg_agi_diff) %>%
#    ggplot(aes(x = year, y = avg_agi_diff, fill = name))+
#   geom_smooth(aes(color = name),se=FALSE)+
#   geom_hline(yintercept = 0)+
#   #geom_point(shape =21, color = "black", size =2)+
#   scale_color_viridis(discrete=TRUE, name="County")+
#   scale_fill_viridis(discrete=TRUE, name="County")+
#   xlab("year")+ylab("Change in 'average gross income'")+bbc_style()
# 
# ex_inc<-addSmallLegend(ex_inc)
# 
# core_family<-D_IRS_06_18 %>% filter(state==13) %>% 
#   filter(name%in%c( "Cobb County", "Clayton County", "DeKalb County","Fulton County", "Gwinnett County",  
#                     "Dekalb County", "De Kalb County")) %>% 
#   mutate(name = case_when(name%in%c("DeKalb County", "Dekalb County", "De Kalb County")~"DeKalb County", 
#                           name%in%c("DeKalb County", "Dekalb County", "De Kalb County")==FALSE~name)) %>%
#   mutate(avg_ex_p_r_in = exempts_in/returns_in,avg_ex_p_ret_out = exempts_out/returns_out, 
#          diff_in_avg = avg_ex_p_r_in-avg_ex_p_ret_out, avg_agi_in = agi_in/exempts_in, 
#          avg_agi_out = agi_out/exempts_out, avg_agi_diff = avg_agi_in-avg_agi_out) %>%
#   select(name, year, returns.d, exempts.d, agi.d, avg_ex_p_r_in, avg_ex_p_ret_out, diff_in_avg,
#          avg_agi_in,avg_agi_out,avg_agi_diff) %>%
#    ggplot(aes(x = year, y = diff_in_avg, fill = name))+
#   geom_smooth(aes(color = name),se=FALSE)+
#   geom_hline(yintercept = 0)+
#   #geom_point(shape =21, color = "black", size =2)+
#   scale_color_brewer(palette = "Paired", name="County")+
#   scale_fill_brewer(palette = "Paired", name="County")+
#   xlab("year")+ylab("Change in 'average family size'")+bbc_style()
# 
# core_family<-addSmallLegend(core_family)
# 
# ex_family<-D_IRS_06_18 %>% filter(state==13) %>% 
#   filter(name%in%c( "Cherokee County","Douglas County", "Fayette County","Henry County","Rockdale County")) %>%
#   mutate(avg_ex_p_r_in = exempts_in/returns_in,avg_ex_p_ret_out = exempts_out/returns_out, 
#          diff_in_avg = avg_ex_p_r_in-avg_ex_p_ret_out, avg_agi_in = agi_in/exempts_in, 
#          avg_agi_out = agi_out/exempts_out, avg_agi_diff = avg_agi_in-avg_agi_out) %>%
#   select(name, year, returns.d, exempts.d, agi.d, avg_ex_p_r_in, avg_ex_p_ret_out, diff_in_avg,
#          avg_agi_in,avg_agi_out,avg_agi_diff) %>%
#   ggplot(aes(x = year, y = diff_in_avg, fill = name))+
#   geom_smooth(aes(color = name),se=FALSE)+
#   geom_hline(yintercept = 0)+
#   #geom_point(shape =21, color = "black", size =2)+
#   scale_color_viridis(discrete=TRUE, name="County")+
#   scale_fill_viridis(discrete=TRUE, name="County")+
#   xlab("year")+ylab("Change in 'average family size'")+
#   xlab("year")+ylab("Change in 'average family size'")+bbc_style()
# 
# ex_family<-addSmallLegend(ex_family)
# 
# core_plt<-ggarrange(core_family, core_inc, ncol=2, common.legend=TRUE) 
# ex_plt<-ggarrange(ex_family, ex_inc, ncol = 2, common.legend=TRUE)
# 
# p<-ggarrange(core_family, ex_family, nrow=2)

core_family<-D_IRS_06_18 %>% filter(state==13) %>% 
  filter(name%in%c( "Cobb County", "Clayton County", "DeKalb County","Fulton County", "Gwinnett County",  
                    "Dekalb County", "De Kalb County")) %>% 
  mutate(name = case_when(name%in%c("DeKalb County", "Dekalb County", "De Kalb County")~"DeKalb County", 
                          name%in%c("DeKalb County", "Dekalb County", "De Kalb County")==FALSE~name)) %>%
  mutate(avg_ex_p_r_in = exempts_in/returns_in,avg_ex_p_ret_out = exempts_out/returns_out, 
         diff_in_avg = avg_ex_p_r_in-avg_ex_p_ret_out, avg_agi_in = agi_in/exempts_in, 
         avg_agi_out = agi_out/exempts_out, avg_agi_diff = avg_agi_in-avg_agi_out) %>%
  select(name, year, returns.d, exempts.d, agi.d, avg_ex_p_r_in, avg_ex_p_ret_out, diff_in_avg,
         avg_agi_in,avg_agi_out,avg_agi_diff) %>% 
  add_column(area="core")

ex_family<-D_IRS_06_18 %>% filter(state==13) %>% 
  filter(name%in%c( "Cherokee County","Douglas County", "Fayette County","Henry County","Rockdale County")) %>%
  mutate(avg_ex_p_r_in = exempts_in/returns_in,avg_ex_p_ret_out = exempts_out/returns_out, 
         diff_in_avg = avg_ex_p_r_in-avg_ex_p_ret_out, avg_agi_in = agi_in/exempts_in, 
         avg_agi_out = agi_out/exempts_out, avg_agi_diff = avg_agi_in-avg_agi_out) %>%
  select(name, year, returns.d, exempts.d, agi.d, avg_ex_p_r_in, avg_ex_p_ret_out, diff_in_avg,
         avg_agi_in,avg_agi_out,avg_agi_diff) %>% add_column(area="ex") 

family_plt<-rbind(core_family, ex_family)%>% 
  mutate(name = str_split(name, " ") %>% 
           lapply(function(x)return(x[1])) %>% unlist)

plt<-family_plt%>%ggplot(aes(x = year, y = diff_in_avg, fill = name,linetype=area))+
  geom_smooth(aes(color = name),se=FALSE)+
  geom_hline(yintercept = 0, color = "black", alpha = .6, size = 1.1)+
  #geom_point(shape =21, color = "black", size =2)+
  scale_color_brewer(palette="Paired", name="County")+
  scale_fill_brewer(palette = "Paired", name="County")+
  xlab("year")+ylab("Change in 'average family size'")+
  xlab("year")+ylab("Change in 'average family size'")+bbc_style()+
  guides(linetype=FALSE)

plt<-addSmallLegend(plt)

plt<-annotate_figure(plt,top = text_grob("Change in family size", size = 16, 
                                  face = "bold"))

annotate_figure(plt,bottom = text_grob("Dashed is exurbs, solid is core", 
                                     size = 11))
```

![](Atl_migration_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

Stone suggests that policy makers sometimes incentivize this trade.
“\[They\] have a deeply misanthropic calculus,” he said. “It’s really
good to have households where there are two prime working-age employed
people who never have babies and never visit their families.”

It’s ideal because those people—known as D.I.N.Ks (double income, no
kids)—pay a lot in taxes and consume few social services.
“Unfortunately, they’re a dead end for the human species,” Stone said.

He listed two ways that cities incentivize D.I.N.Ks to move in and
families to move out. First is limited zoning, typically in the form of
single-family housing. “We like to think of single-family housing as
family-friendly zoning, but this isn’t true,” Stone said.

Atlanta prioritizes single-family housing. About 63% of the housing
available in the city is reserved for single families, while only 37% is
usable for any other kind of housing.

``` r
####checking landuse in Atlanta. most of it is SFR
shape_landuse_ATL <- st_read(dsn = "~/Desktop/Datasets/migration_politics/LandUse_Future/", 
                    layer = "LandUse_Future", quiet= TRUE)

shape_landuse_ATL_f<-shape_landuse_ATL %>%
  mutate(sfr_or_not = case_when(LANDUSEDES=="Single-Family Residential"~"SFR",
                                LANDUSEDES%in%c("Low-Density Commercial",
                                                "Industrial",
                                                "Office/Institutional",
                                                "High-Density Commercial")~
                                  "Commercial",
                                LANDUSEDES%in%c("Medium-Density Residential",
                                                "Low-Density Residential",
                                                "Mixed-Use",
                                                "High-Density Residential",
                                                "Low-Density Mixed-Use",
                                                "Medium-Density Mixed-Use",
                                                "High-Density Mixed-Use",
                                                "Very High-Density Residential",
                                                "Mixed Use-High Density",
                                                "Mixed Use-Low Density"
                                                )~"Other_housing",
                                (LANDUSEDES=="Single-Family Residential")== 
                                  FALSE~"Other")
         )

plt<-shape_landuse_ATL_f %>% ggplot(aes(color = sfr_or_not, fill = sfr_or_not)) +geom_sf()+
  scale_color_brewer(name="Zoning type", palette = "Dark2")+
  scale_fill_brewer( name="Zoning type", palette = "Dark2")+bbc_style()+
  theme(axis.text.x=element_blank(),
          axis.text.y=element_blank())

plt<-addSmallLegend(plt)

annotate_figure(plt,top = text_grob("Atlanta plurality SFR", size = 16, 
                                  face = "bold"))
```

![](Atl_migration_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

Importantly, housing types are segregated. Carnathan told the AJC that
“You have lots of detached single-family housing stock and then you’ll
have big towering apartment buildings, and you just don’t have a lot in
between,” and that’s exactly what’s reflected in the map. There are pink
blocks and dark lavender, but almost no areas checkered with both.

Nearby Sandy Springs makes a similar choice in its housing allocation,
according to data reporting from the New York Times. 85% of their
housing is limited to single-family homes—one of the highest rates in
the country.

According to that story, the higher density that comes with multi-family
housing is viewed by environmentalists “as an antidote to sprawling
development patterns that feed gridlock and auto emissions,” by planners
as “an essential condition to support public transit,” and by economists
as “the best means of making high cost cities more affordable.”

Stone’s second point is the importance of multi-mode transportation. “A
lot of families don’t have enough cars to shuttle every kid, everywhere,
all the time.” Yet, again, Atlanta falls short of what would be good for
families. According to Census data, over 97% of Atlantans get to work in
a personal vehicle. That’s the third largest percentage among cities
with more than 2 million people.

Smart Growth America, a coalition of more than 70 national and local
advocacy groups, including the National Defense Resources Council and
the AARP, sums these points up, saying: “Often, (supporting families is)
about simply providing more choice where we’ve favored one
transportation option of housing style to the detriment of the greater
good.”

Covid isn’t making this any easier. In the last two months, 228,352
Georgian’s filed unemployment claims—31% of Georgia’s workforce.
Carnathan is “viewing this similarly to what happened in the Great
Recession” and doesn’t expect the domestic trend the AJC discovered to
change.

On the international front, however, it will almost certainly be
exacerbated, he said. According to U.S. Census, the majority of recent
international migration has come from Asia, the continent first affected
by Covid-19.

The ARC and other experts agree that domestic migration decreases in a
recession. With policies and circumstances (like a global pandemic)
decreasing international migration, and decreasing birth rates affecting
natural increases in population, growing the local economy by bringing
outside workers is looking like a more difficult proposition.

According to Carnathan, “the demographics are kind of lining up to show
us that we’re going to have a harder time attracting talent to our
borders, we need to pay attention to growing the talent we
have.”

<!-- ```{r echo=FALSE} -->

<!-- D_acs_in %>% filter(source%in%c("c2c","acs")==FALSE&name_t%in%c("Fulton", "DeKalb", "Cobb","Gwinnett","Clayton"))%>%  -->

<!--   group_by(source, year) %>% summarise( net_flow = sum(net_flow)) %>%  -->

<!--   ggplot(aes(x = year, y = net_flow, fill = source))+ -->

<!--   geom_smooth(aes(color = source),se=FALSE)+ -->

<!--   geom_point(shape =21, color = "black", size =2)+ -->

<!--   scale_color_viridis(discrete = T, labels = c("ACS", "IRS", "PEP"))+ -->

<!--   scale_fill_viridis(discrete = T, labels = c("ACS", "IRS", "PEP"))+ -->

<!--   ylab("Domestic migration")+ggtitle("Census domestic migration and IRS migration into the Atlanta core")+ -->

<!--   ylim(-17000,30000)+geom_hline(yintercept = 0)+geom_hline(yintercept = 0, color = "#ff7a61")+ -->

<!--   bbc_style() -->

<!-- ``` -->

<!-- The IRS paints a more negative picture than the Census data. While the shapes of the curves are nearly identical, a reasurring sanity check, the IRS data estimates between 5,000 and 10,000 fewer migrants a year, a number which varies over time.  -->

<!-- The IRS data puts migration into the Atlanta core as having been nearly 0 from the onset of the Great Recession until around 2016, and negative since. The difference between the two is important and comes from two main sources. -->

<!-- IRS data, by definition, comes from people who file taxes. The data counts people who filed returns in one state last year and another state this year. Non-filers will not show up. In general, non-filers include the young, the unemployed, students, and retirees. However, as a measure of the active workforce newly added to the Atlanta core, it is a good metric. So, while domestic migration is recently negative, domestic migration of workers has been zero for a long time. -->

<!-- The second component of the difference comes from temporary immigrants. You must have filed two tax returns to show up in this data. If you were here for one year but not the next, you won't show up in the IRS data. This indicates that, to some degree, migrants to the Atlanta core have been temporary migrants.  -->

<!-- How can we distinguish between these cases? -->

<!-- ```{r} -->

<!-- D_acs_in %>% filter(source%in%c("c2c","acs")==FALSE&name_t%in%c("Cherokee", "Douglas", "Fayette","Henry","Rockdale"))%>% -->

<!--   group_by(source, year) %>% summarise( net_flow = sum(net_flow)) %>% ggplot(aes(x = year, y = net_flow, fill = source))+ -->

<!--   geom_smooth(aes(color = source),se=FALSE)+ -->

<!--   geom_point(shape =21, color = "black", size =2)+ -->

<!--   scale_color_viridis(discrete = T, labels = c("ACS", "IRS", "PEP"))+ -->

<!--   scale_fill_viridis(discrete = T, labels = c("ACS", "IRS", "PEP"))+ -->

<!--   ylab("Domestic migration")+ggtitle("Census domestic migration and IRS migration into the Atlanta core")+ylim(-17000,30000)+geom_hline(yintercept = 0, color = "#ff7a61")+bbc_style() -->

<!-- ``` -->

<!-- The lack of a difference between IRS data and PEP data in the exurbs gives us a hint. Low-income movers and the unemployed have, by definition, less disposable income to spend on rent and the necessities of living. If it was the case that low-income movers were driving the gap between IRS data and PEP data, we would expect to see some sort of a gap in the parts of Atlanta that are more affordable. The exurbs, in median, mean, and minimum, are cheaper, yet that's not what we see. -->

<!-- In the positive direction, the Census PEP data by domestic and international migration shown above makes clear that international immigration into the core counties is substantial but nearly non-existent in the exurbs. The gap between the IRS data and the PEP data is almost exactly equal to the international immigration counted by the PEP data.  -->

<!-- It seems, then, that the majority of the gap between the IRS data and PEP data comes from temporary migrants who stay in the US for one year, and leave during the next. -->

<!-- This matters because migration is possibly the most important indicator of economic prosperity in the present and potential prosperity in the future. With decreasing international migration and national policies intended to curb it, temporary international migration cannot be counted on as a sustained form of growth.  -->

<!-- Natural increases from births outpacing deaths are so low that current projections estimate there will student shortages in the hundreds of thousands in Georgia schools in coming years. If combined with sustained negative domestic migration, something likely to continue or worsen given the looming recession, population growth in the Atlanta area could soon become an economic problem. -->

<!-- Yet, the prevailing narrative is an optimistic one, of growth and good fortune, both measured and sustained by the growing population. There's no assured cause for concern, but there is a need for clear eyes and re-evaluation. -->

<!-- There are some other interesting findings including where commuters commute to (increasingly the exurbs) and where international immigrants migrate from (mostly Asia with a substantial amount from Central and South America, as well). There is also evidence, produced by researchers elsewhere, that the Atlanta core's domestic outmigration is a Black reverse-migration caused by increasing prices. All of these could be used in the piece. -->

<!-- Here is the SFR plot -->

<!-- And the perc of single family -->

<!-- ```{r} -->

<!-- shape_landuse_ATL_f %>%data.frame %>% select(-geometry) %>%  filter(sfr_or_not%in%c("SFR","Other_housing")) %>% group_by(sfr_or_not) %>% -->

<!--   summarise(acres_tot = sum(ACRES)) %>% mutate(perc_zone=acres_tot/sum(acres_tot))%>% arrange(perc_zone) %>%  -->

<!--   mutate(`Percent Single Family` = as.character(perc_zone*100) %>% -->

<!--            str_sub(1,4) %>% str_c(.,"%"), -->

<!--          `Type of Residence` = sfr_or_not, -->

<!--          `Total Acres` = acres_tot) %>%  -->

<!--   select(`Type of Residence`,`Total Acres`,`Percent Single Family`) -->

<!-- ``` -->

<!-- Here's the data on commuting by car -->

<!-- ```{r} -->

<!-- D_acs_trav <-  get_acs(geography = "metropolitan statistical area/micropolitan statistical area", -->

<!--                   variables = c(car="B08006_002E", public="B08006_008E",bike="B08006_014E"), year = 2018) -->

<!-- #3rd among cities with more 2 million people, 11 cities -->

<!-- D_acs_trav_f<-D_acs_trav %>% mutate(variable = case_when(variable=="B08006_002"~"car", variable=="B08006_008"~"public", -->

<!--                                            variable =="B08006_014"~"bike")) %>% select(-moe) %>%  -->

<!--   pivot_wider(names_from = variable, values_from=estimate) %>%  -->

<!--   mutate(total = car+public+bike, car_perc= car/total, public_perc = public/total, bike_perc = bike/total) -->

<!-- D_acs_trav_f %>% filter(total>2000000) %>% arrange(desc(car_perc)) %>% add_column(`Rank of percent of people who commute to work by car`=1:nrow(.)) %>% -->

<!--   mutate(`Percent commuting by car`=as.character(car_perc*100) %>% str_sub(1,4) %>% str_c(.,"%")) %>% -->

<!--   select(`Metro area`= NAME,  -->

<!--          `Rank of percent of people who commute to work by car`,  -->

<!--          `Percent commuting by car`) -->

<!-- ``` -->

<!-- Here are the plots that give why it's changing -->
