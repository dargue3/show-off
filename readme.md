Just wanted to give a brief explanation about what’s going on. This code is used in a team-sports management web app. In particular, this controls how the stats tables are built for a basketball team.

Stats.vue -> defines the template and CSS

AbstractStat.js -> a mixin that controls the compilation process for every sport

Basketball.vue -> defines how a basketball stat table looks, calculates advanced stats

Stats.vue is a Vue.js component that can be dropped in anywhere; given a sport, type, and some raw stats, and will output a responsive stat table. The beauty, and the reason I’m proud of it, is the reusability of the code between sports. Just dynamically activate a different component, perhaps Soccer.vue, and the stats table will be tailored for soccer.

In this example, you can see Basketball.vue has a bunch of hooks that are used to edit the stats during different segments of their compilation process; functions such as `editPlayersStatsBeforeAddingThemToTheirSeasonTotals()`. 

This allows you to calculate advanced stats for sports no matter where that happens in the compilation process. These hooks are all called from AbstractStat.js, and depending on which sport component has been activated in Stats.vue, calls the correct functions.

Also found in Basketball.vue are a bunch of closure definitions for dynamically calculating things such as: table header classes, tooltips, stat key names, rounding, etc.

Once the compilation process has finished, Stats.vue renders its DOM, calling the many closures to dynamically build a nice little stats table.


Bonus features:
Listeners for scrolling on tables, shows indicators when stat columns are overflowed and require scrolling to see them.

‘Search by name’ filters the v-for to only include rows with matching first/last names

Click to sort the table by stat key ascending or descending (red is the current sort key)