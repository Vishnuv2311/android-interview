# How to Communicate Between Two Fragments in Android

Communicating between two Fragments in Android can be achieved through several methods. Here are some common approaches:

## 1. Using ViewModel

The ViewModel approach is recommended when both Fragments are part of the same Activity. You can share data between Fragments using a shared ViewModel. Here’s how to implement it:

```kotlin
class SharedViewModel : ViewModel() {
    val selected = MutableLiveData<Item>()
}

class FragmentA : Fragment() {
    private lateinit var viewModel: SharedViewModel

    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {
        viewModel = ViewModelProvider(requireActivity()).get(SharedViewModel::class.java)
        // Set up your UI and listeners
    }
}

class FragmentB : Fragment() {
    private lateinit var viewModel: SharedViewModel

    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {
        viewModel = ViewModelProvider(requireActivity()).get(SharedViewModel::class.java)
        viewModel.selected.observe(viewLifecycleOwner, Observer { item ->
            // Update UI based on the selected item
        })
    }
}
```

## 2. Using Interface Callbacks

Another common way to communicate between Fragments is through interface callbacks. This method allows a Fragment to send data to its host Activity, which can then pass that data to another Fragment.

```kotlin
interface OnDataPass {
    fun onDataPass(data: String)
}

class FragmentA : Fragment() {
    private lateinit var dataPasser: OnDataPass

    override fun onAttach(context: Context) {
        super.onAttach(context)
        dataPasser = context as OnDataPass
    }

    private fun passData() {
        dataPasser.onDataPass("Data from Fragment A")
    }
}

class FragmentB : Fragment(), OnDataPass {
    override fun onDataPass(data: String) {
        // Handle the data received from Fragment A
    }
}
```

## 3. Using FragmentManager

You can also communicate directly between Fragments using FragmentManager. This method is less preferred as it tightly couples the Fragments, but it can be useful in certain scenarios.

```kotlin
class FragmentA : Fragment() {
    private fun sendDataToFragmentB() {
        val fragmentB = FragmentB()
        val bundle = Bundle()
        bundle.putString("key", "value from Fragment A")
        fragmentB.arguments = bundle

        fragmentManager?.beginTransaction()
            ?.replace(R.id.fragment_container, fragmentB)
            ?.addToBackStack(null)
            ?.commit()
    }
}

class FragmentB : Fragment() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val data = arguments?.getString("key")
        // Use the data received from Fragment A
    }
}
```

These methods provide flexibility in how you can manage communication between Fragments in your Android applications. Choose the one that best fits your architecture and use case.
