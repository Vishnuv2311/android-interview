# What is Fragment and its Lifecycle?

## What is a Fragment?
A **Fragment** in Android is a modular section of an activity, which has its own lifecycle, receives its own input events, and can be added or removed while the activity is running. It allows developers to build dynamic and flexible UI designs that can adapt to different screen sizes.

Fragments are often used in multi-pane UI layouts and for reusable UI components in various parts of an application.

## Fragment Lifecycle
A fragment’s lifecycle is closely tied to its host activity's lifecycle, but it has additional states:

1. **onAttach(Context context)** - Called when the fragment is attached to its parent activity.
2. **onCreate(Bundle savedInstanceState)** - Initializes fragment, similar to an Activity’s `onCreate()`.
3. **onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState)** - Called to create the fragment’s UI.
4. **onViewCreated(View view, Bundle savedInstanceState)** - Called after `onCreateView()`, used to initialize UI elements.
5. **onStart()** - The fragment becomes visible but not yet interactive.
6. **onResume()** - The fragment is now active and interactive.
7. **onPause()** - The fragment is partially visible but no longer interactive.
8. **onStop()** - The fragment is no longer visible.
9. **onDestroyView()** - The fragment’s UI is removed from memory.
10. **onDestroy()** - Called when the fragment is being completely destroyed.
11. **onDetach()** - The fragment is detached from its parent activity.

## Key Points
- Fragments must always be hosted in an activity.
- They allow dynamic UI changes and flexible layouts.
- Fragment transactions (`add`, `replace`, `remove`) are handled using the FragmentManager.
- Fragments improve modularity and reusability in Android applications.
