# Difference between FragmentPagerAdapter vs FragmentStatePagerAdapter

In Android, `FragmentPagerAdapter` and `FragmentStatePagerAdapter` are both used with `ViewPager` to manage fragments. However, they have key differences in how they handle fragment lifecycles and memory management.

## 1. FragmentPagerAdapter
- Keeps all fragments in memory, which can lead to high memory usage.
- Fragments are not destroyed but only detached when they go off-screen.
- Suitable for a small number of static fragments.
- Use case: When the number of pages is fixed and limited, such as a tabbed interface with a few static fragments.

## 2. FragmentStatePagerAdapter
- Destroys fragments that go off-screen to save memory.
- Saves the state of each fragment, recreating it when needed.
- Suitable for large numbers of dynamically loaded pages.
- Use case: When working with a large number of fragments, such as dynamically loading content from a database or API.

## Which one to use?
- If you have a **small, fixed** number of fragments, use `FragmentPagerAdapter`.
- If you have a **large, dynamic** number of fragments, use `FragmentStatePagerAdapter` to save memory.

**Note:** As of AndroidX, both are deprecated, and `ViewPager2` with `FragmentStateAdapter` should be used instead.
