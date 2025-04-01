# Explain the Role of RecyclerView.Adapter and RecyclerView.ViewHolder

In Android, `RecyclerView.Adapter` and `RecyclerView.ViewHolder` are essential components when working with `RecyclerView`, which is a more efficient and flexible replacement for `ListView`.

## RecyclerView.Adapter
The `RecyclerView.Adapter` is responsible for:
- Creating `ViewHolder` instances as needed.
- Binding data to `ViewHolder` at the correct position.
- Managing the data set and notifying the `RecyclerView` of data changes.

### Key Methods of RecyclerView.Adapter
- `onCreateViewHolder(ViewGroup parent, int viewType)`: Creates a new `ViewHolder` instance.
- `onBindViewHolder(VH holder, int position)`: Binds data to the `ViewHolder` at the given position.
- `getItemCount()`: Returns the total number of items in the data set.

## RecyclerView.ViewHolder
The `RecyclerView.ViewHolder` is responsible for:
- Holding the view references for an item.
- Avoiding unnecessary calls to `findViewById()` by caching references.

### Example Implementation

```kotlin
class MyAdapter(private val itemList: List<String>) : RecyclerView.Adapter<MyAdapter.MyViewHolder>() {

    class MyViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
        val textView: TextView = itemView.findViewById(R.id.textView)
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): MyViewHolder {
        val view = LayoutInflater.from(parent.context).inflate(R.layout.item_layout, parent, false)
        return MyViewHolder(view)
    }

    override fun onBindViewHolder(holder: MyViewHolder, position: Int) {
        holder.textView.text = itemList[position]
    }

    override fun getItemCount(): Int {
        return itemList.size
    }
}
```

## Summary
- `RecyclerView.Adapter` acts as a bridge between the data source and UI.
- `RecyclerView.ViewHolder` holds and manages item views for better performance.
- Using `ViewHolder` reduces unnecessary calls to `findViewById()`.

These components together improve performance by reusing views and minimizing unnecessary object creation.
