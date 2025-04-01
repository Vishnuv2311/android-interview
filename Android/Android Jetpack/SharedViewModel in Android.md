# SharedViewModel in Android

## What is SharedViewModel?
A `SharedViewModel` is a `ViewModel` that is shared between multiple fragments or activities. It allows fragments or activities to communicate with each other while following the MVVM architecture.

## Why use SharedViewModel?
- Helps share data between fragments without tightly coupling them.
- Reduces the need for callbacks, interfaces, or event buses.
- Preserves data across configuration changes.

## Implementation of SharedViewModel

1. **Create a SharedViewModel class**
```kotlin
class SharedViewModel : ViewModel() {
    private val _sharedData = MutableLiveData<String>()
    val sharedData: LiveData<String> get() = _sharedData

    fun updateData(data: String) {
        _sharedData.value = data
    }
}
```

2. **Use SharedViewModel in Fragments**

- **Fragment A (Sender)**
```kotlin
class FragmentA : Fragment() {
    private lateinit var viewModel: SharedViewModel

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?
    ): View? {
        val view = inflater.inflate(R.layout.fragment_a, container, false)
        viewModel = ViewModelProvider(requireActivity()).get(SharedViewModel::class.java)

        view.findViewById<Button>(R.id.sendButton).setOnClickListener {
            viewModel.updateData("Hello from Fragment A")
        }
        return view
    }
}
```

- **Fragment B (Receiver)**
```kotlin
class FragmentB : Fragment() {
    private lateinit var viewModel: SharedViewModel

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?
    ): View? {
        val view = inflater.inflate(R.layout.fragment_b, container, false)
        viewModel = ViewModelProvider(requireActivity()).get(SharedViewModel::class.java)

        viewModel.sharedData.observe(viewLifecycleOwner, Observer { data ->
            view.findViewById<TextView>(R.id.textView).text = data
        })
        return view
    }
}
```

## Explanation
- `ViewModelProvider(requireActivity())`: Ensures that both fragments use the same instance of `SharedViewModel`.
- `LiveData`: Observes changes and updates the UI in Fragment B when Fragment A updates the data.
- Helps achieve fragment communication in a clean, lifecycle-aware way.
