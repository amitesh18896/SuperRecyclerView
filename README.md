# SuperRecyclerView

Maven Central Build Status Android Arsenal


##Description


This is an attempt to make RecyclerView easier to use.


Features built in:


ProgressBar while adapter hasn't been set


EmptyView if adapter is empty


SwipeRefreshLayout (Google's one)


Infinite scrolling, when you reach the X last item, load more of them.


Swipe To Dismiss or Swipe To Remove


Sticky headers (via Eowise, see sample)



##Integration



Just add it to you dependencies



    compile 'com.malinskiy:superrecyclerview:$version'
    
    
    
    ##Usage
    
    

Use directly SuperRecyclerView:


 <com.malinskiy.superrecyclerview.SuperRecyclerView
 
 
            android:id="@+id/list"
            
            
            xmlns:app="http://schemas.android.com/apk/res-auto"
            
            
            android:layout_width="match_parent"
            
            
            android:layout_height="match_parent"
            
            
            app:layout_empty="@layout/emptyview"
            
            
            app:layout_moreProgress="@layout/view_more_progress"
            
            
            app:mainLayoutId="@layout/layout_recyclerview_verticalscroll"
            
            
            app:recyclerClipToPadding="false"
            
            
            app:recyclerPadding="16dp"
            
            
            app:scrollbarStyle="insideInset"/>
            
            
            
            Current Attributes supported:
            
            
            
            <attr name="layout_empty" format="reference"/>
            
            
    <attr name="layout_moreProgress" format="reference"/>
    
    
    <attr name="layout_progress" format="reference"/>
    
    
    <attr name="recyclerClipToPadding" format="boolean"/>
    
    
    <attr name="recyclerPadding" format="dimension"/>
    
    
    <attr name="recyclerPaddingTop" format="dimension"/>
    
    
    <attr name="recyclerPaddingBottom" format="dimension"/>
    
    
    <attr name="recyclerPaddingLeft" format="dimension"/>
    
    
    <attr name="recyclerPaddingRight" format="dimension"/>
    
    
    <attr name="scrollbarStyle">
    
    
        <flag name="insideOverlay" value="0x0"/>
        
        
        <flag name="insideInset" value="0x01000000"/>
        
        
        <flag name="outsideOverlay" value="0x02000000"/>
        
        
        <flag name="outsideInset" value="0x03000000"/>
        
        
    </attr>
    
    

    <attr name="mainLayoutId" format="reference"/>
    
    
    
    ##SuperRecyclerView Java Usage
    
    
    
    recycler.setRefreshListener(new SwipeRefreshLayout.OnRefreshListener {
    
    
      @Override
      
      
      public void onRefresh() {
      
      
          // Do your refresh
          
          
      });
      
      

    // when there is only 10 items to see in the recycler, this is triggered
    
    
    recycler.setupMoreListener(new OnMoreListener() {
    
    
      @Override
      
      
      public void onMoreAsked(int numberOfItems, int numberBeforeMore, int currentItemPos) {
      
      
        // Fetch more from Api or DB
        
        
      }}, 10);
      
      

    recycler.setupSwipeToDismiss(new SwipeDismissListViewTouchListener.DismissCallbacks() {
    
    
    
      @Override
      
      
      public boolean canDismiss(int position) {
      
      
        return true
        
        
      }
      

      @Override
      
      
      public void onDismiss(RecyclerView recyclerView, int[] reverseSortedPositions) {
      
      
        // Do your stuff like call an Api or update your db
        
        
        
      }});
      
      
      
      ##Scrollbars RecyclerView currently doesn't support setting scrollbars from code that's why I can't parse custom 
      
      
      attributes. You have to use appropriate mainLayoutId attribute to have scrollbars visible.
      
      

Vertical scrollbars



<com.malinskiy.superrecyclerview.SuperRecyclerView


     app:mainLayoutId="@layout/layout_recyclerview_verticalscroll"
     
     
     app:scrollbarStyle="insideInset"
     
     
     .../>
     
     
     
     Horizontal scrollbars
     
     
<com.malinskiy.superrecyclerview.SuperRecyclerView


     app:mainLayoutId="@layout/layout_recyclerview_horizontalscroll"
     
     
     app:scrollbarStyle="insideInset"
     
     
     .../>
     
     
     
     ##Swipe layout
     
     

You should always assign android:id to @id/recyclerview_swipe. Note that it's a reference to an already


defined id, so don't use @+id


The SwipeLayout can only have 2 children that are instances of ViewGroup, e.g. LinearLayout, RelativeLayout, 


GridLayout


The first child is the bottom view, the second child is the top view



Your adapter should extend BaseSwipeAdapter class


Do not setup swipe to dismiss and use swipe layout at the same time. If you do - a kitten will cry somewhere.



Item example:


<com.malinskiy.superrecyclerview.swipe.SwipeLayout


    android:id="@id/recyclerview_swipe"
    
    
    xmlns:swipe="http://schemas.android.com/apk/res-auto"
    
    
    android:layout_width="match_parent"
    
    
    android:layout_height="wrap_content"
    
    
    swipe:horizontalSwipeOffset="16dp">
    
    

    <LinearLayout
    
    
        ...
        
        
    </LinearLayout>
    
    

    <LinearLayout
    
    
        ...
        
        
    </LinearLayout>
    
    

</com.malinskiy.superrecyclerview.swipe.SwipeLayout>



Custom attributes supported:


<attr name="drag_edge" format="enum">


        <enum name="left" value="0"/>
        
        
        <enum name="right" value="1"/>
        
        
        <enum name="top" value="2"/>
        
        
        <enum name="bottom" value="3"/>
        
        
    </attr>
    
    
    <attr name="horizontalSwipeOffset" format="dimension"/>
    
    
    <attr name="verticalSwipeOffset" format="dimension"/>
    
    
    
    <attr name="show_mode" format="enum">
    
    
        <enum name="lay_down" value="0"/>
        
        
        <enum name="pull_out" value="1"/>
        
        
    </attr>
    
    
    ####Sample java
    
    

Proguard


-dontwarn com.malinskiy.superrecyclerview.SwipeDismissRecyclerViewTouchListener*



##Thanks Jake Warthon for implementation of SwipeToDismiss via NineOldAndroids



Eowise for implementation of sticky headers



Quentin Dommerc for inspiration



代码家 for swipe layout implementation



##License


opyright (c) 2016 Anton Malinskiy


Licensed under the Apache License, Version 2.0 (the "License");



you may not use this file except in compliance with the License.


You may obtain a copy of the License at


   http://www.apache.org/licenses/LICENSE-2.0
   
   

Unless required by applicable law or agreed to in writing, software


distributed under the License is distributed on an "AS IS" BASIS,


WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.


See the License for the specific language governing permissions and


limitations under the License.



Come on, don't tell me you read that..


            
            
            
            
