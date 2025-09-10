## Requeuing-Round-Wise

- try here : `https://leetcode.com/problems/dota2-senate/description/`
- About the round-wise dequing and then requeue the elgibile participant for the next round : Next round `+n` so that the participant left in prev round {if didn't get paired} with another of other party then they rest in q {with smaller turn value } and next round participants are added with the `curr_turnVal + n` for next round
- Extra participants of any of the 2 groups are given chance in the next round {having smaller turn val}

 
 ```cpp
    class Solution {
    public: 
    // senator type ques 
        string predictPartyVictory(string senate) {
            int n = senate.length();
            queue<int> rq;
            queue<int> dq;
            for (int i = 0 ; i < n ; i++) {
                if (senate[i] == 'R') {
                    rq.push(i) ;
                }else {
                    dq.push(i) ;
                }
            }
            while (!rq.empty() && !dq.empty()) {
                int sz1 = rq.size(); int sz2 = dq.size();
                for (int j = 0 ; j < min(sz1 ,sz2) ; j++) {
                    int ri = rq.front(); rq.pop();
                    int di = dq.front(); dq.pop();
                    if (ri < di) {
                        rq.push(ri + n);
                    }else {
                        dq.push(di + n) ;
                    }
                }
            }
            if (dq.empty() && rq.empty()) {
                if (senate[0] == 'R') {
                    return "Radiant"  ;
                }else {
                    return "Dire"  ;
                }
            }else if (!dq.empty()) {
                return "Dire"  ;
            }else {
                return "Radiant"  ;
            }
        }
    };
 ```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N)    |    In worst case if any ele may left at one first stage {of dominant party} then gets to remove any chance for the rest of the rounds and becomes the 1st member of next round , & always get to reenqueued, so eliminating all other n senators|
| 🧠 SPACE |  O(N)          |    R_queue, D_queue       |
