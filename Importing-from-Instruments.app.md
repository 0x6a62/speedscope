There are two supported methods for importing from [Instruments.app](https://help.apple.com/instruments/mac/current/): importing Time Profiler .trace files, and importing via deep copy.

## Importing Time Profiler .trace files

To record a time profile using Instruments.app, first select "Time Profiler" from the list of profiling templates.

![Instruments.app profiling template selection screen](https://i.imgur.com/gy4hTkD.png)

Select the target you want to profile.

![Selecting the profile](https://i.imgur.com/XWKnbk4.png)

Click the record button.

![Clicking record](https://i.imgur.com/VBoqJu8.png)

When you're done recording, hit the stop button.

![Clicking stop](https://i.imgur.com/lQyXEY7.png)

Then save the profile as a `.trace` file.

![Saving a profile](https://i.imgur.com/9VKeB0G.png)

If you drag and drop the resulting file into speedscope, it should load the profile.

At time of writing, selecting the file via "browse" or running `speedscope /path/to/Instruments.trace` won't work. See https://github.com/jlfwong/speedscope/issues/97

## Importing via deep copy

After recording either a Time Profiler profile or an Allocations profile, select the root row of the table view. Then select "Edit -> Deep Copy" from the main menu.

![Deep copy menu item](https://i.imgur.com/Ehl0u5K.png)

This will copy a tree containing aggregate statistics about the profile onto your clipboard. Now visit https://www.speedscope.app and paste. Note that this method only carries aggregate statistics, rather than time-ordered samples, so you the time ordered view and the left heavy view will look similar.