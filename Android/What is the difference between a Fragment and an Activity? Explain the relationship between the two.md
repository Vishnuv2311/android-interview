# Difference Between Fragment and Activity

## Activity:
- An `Activity` is a single screen in an Android application that acts as an entry point for user interaction.
- It manages the UI components and user interactions.
- It has its own lifecycle managed by the Android OS.
- Typically, an app consists of multiple activities that are navigated using intents.

## Fragment:
- A `Fragment` is a modular UI component that is a part of an `Activity`.
- It is reusable and can be combined with other fragments to create a dynamic UI.
- It has its own lifecycle, but it is dependent on the hosting activity.
- Fragments are useful for building multi-pane layouts in tablets and flexible UI designs.

## Relationship Between Activity and Fragment:
- A `Fragment` must be hosted inside an `Activity` and cannot exist independently.
- An `Activity` can contain multiple fragments, allowing for a more modular and reusable UI.
- Fragments communicate with their host activity using interfaces or shared `ViewModel`s.
- The lifecycle of a `Fragment` is directly influenced by the lifecycle of its parent `Activity`.

## Example:
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Adding a fragment dynamically
        supportFragmentManager.beginTransaction()
            .replace(R.id.fragment_container, SampleFragment())
            .commit()
    }
}

class SampleFragment : Fragment(R.layout.fragment_sample)
```

This demonstrates how an `Activity` can host a `Fragment`, allowing for modular UI development.
