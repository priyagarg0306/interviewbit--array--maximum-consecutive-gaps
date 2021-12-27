# interviewbit--array--maximum-consecutive-gaps

------> Question:

Given an unsorted array, find the maximum difference between the successive elements in its sorted form.

Try to solve it in linear time/space.

Example :

Input : [1, 10, 5]
Output : 5 
Return 0 if the array contains less than 2 elements.

You may assume that all the elements in the array are non-negative integers and fit in the 32-bit signed integer range.
You may also assume that the difference will not overflow.

-----> Code:

int Solution::maximumGap(const vector<int> &v) {
  
    int n=v.size();

    if(n<2){
        return 0;
    }
    int maxi=*max_element(v.begin(),v.end());
    int mini=*min_element(v.begin(),v.end());

    vector<int> bmax(n-1,INT_MIN), bmin(n-1,INT_MAX);

    float gap=(float)(maxi-mini)/(float)(n-1);

    for(int i=0;i<n;i++){
        if(v[i]==maxi || v[i]==mini){
            continue;
        }

        int index=(v[i]-mini)/gap;
        bmax[index]=max(bmax[index],v[i]);
        bmin[index]=min(bmin[index],v[i]);
    }

    int p=mini,ans=0;

    for(int i=0;i<n-1;i++){
        if(bmin[i]==INT_MAX){
            continue;
        }

        ans=max(ans,bmin[i]-p);
        p=bmax[i];
    }

    ans=max(ans,maxi-p);

    return ans;
}
