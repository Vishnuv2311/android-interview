# How do you share ViewModel between Fragments in Android?

In Android, you can share a ViewModel between multiple Fragments using the **Activity scope**. This allows different Fragments to communicate and share data while maintaining lifecycle awareness.

## Steps to Share a ViewModel

1. **Create a Shared ViewModel**
   ```kotlin
   class SharedViewModel : ViewModel() {
       private val _selectedData = MutableLiveData<String>()
       val selectedData: LiveData<String> get() = _selectedData

       fun selectData(data: String) {
           _selectedData.value = data
       }
   }
   ```

2. **Access the Shared ViewModel in Fragments**
   ```kotlin
   class FirstFragment : Fragment() {
       private val viewModel: SharedViewModel by activityViewModels()

       override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
           super.onViewCreated(view, savedInstanceState)
           
           viewModel.selectData("Hello from FirstFragment")
       }
   }

   class SecondFragment : Fragment() {
       private val viewModel: SharedViewModel by activityViewModels()

       override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
           super.onViewCreated(view, savedInstanceState)

           viewModel.selectedData.observe(viewLifecycleOwner) { data ->
               // Use the shared data
               Log.d("SecondFragment", "Received: $data")
           }
       }
   }
   ```

3. **Ensure Both Fragments are Hosted in the Same Activity**
   ```kotlin
   class SharedViewModelActivity : AppCompatActivity() {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_main)
       }
   }
   ```

## Explanation
- The `SharedViewModel` is created at the **Activity level** using `by activityViewModels()`, ensuring both Fragments share the same instance.
- `FirstFragment` updates the `LiveData` in the ViewModel.
- `SecondFragment` observes the `LiveData` and reacts to changes.

This approach is particularly useful for UI interactions where multiple fragments need to share state or communicate efficiently.
