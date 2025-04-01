# How to Update a Specific Item in RecyclerView

Updating a specific item in a `RecyclerView` can be done efficiently using `notifyItemChanged()`. Here’s how you can do it:

## Steps to Update a Specific Item:
  
1. **Modify the Data**: Update the specific item in your data list.
2. **Notify the Adapter**: Use `notifyItemChanged(position)` to refresh only the modified item.

## Example Code:

```kotlin
class MyAdapter(private val itemList: MutableList<String>) : RecyclerView.Adapter<MyAdapter.MyViewHolder>() {

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

    override fun getItemCount(): Int = itemList.size

    fun updateItem(position: Int, newItem: String) {
        itemList[position] = newItem
        notifyItemChanged(position)
    }
}
```

## Alternative Methods:
- Use `DiffUtil` for more efficient updates.
- Call `notifyItemInserted(position)` or `notifyItemRemoved(position)` when adding/removing items.
