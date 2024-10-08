# Minimum-Cost-for-Cutting-Cake-I

There is an m x n cake that needs to be cut into 1 x 1 pieces.
You are given integers m, n, and two arrays:

horizontalCut of size m - 1, where horizontalCut[i] represents the cost to cut along the horizontal line i.
verticalCut of size n - 1, where verticalCut[j] represents the cost to cut along the vertical line j.
In one operation, you can choose any piece of cake that is not yet a 1 x 1 square and perform one of the following cuts:

Cut along a horizontal line i at a cost of horizontalCut[i].
Cut along a vertical line j at a cost of verticalCut[j].
After the cut, the piece of cake is divided into two distinct pieces.

The cost of a cut depends only on the initial cost of the line and does not change.
Return the minimum total cost to cut the entire cake into 1 x 1 pieces.

class Solution:

    def minimumCost(self, m: int, n: int, h: List[int], v: List[int]) -> int:
        h, v = sorted(h), sorted(v)

        @cache
        def calc(hK, vK):
            if h == [] or v == []:
                return sum(h)*hK + sum(v)*vK
            
            q = h.pop()
            res1 = q*hK + calc(hK, vK+1)
            h.append(q)
            q = v.pop()
            res2 = q*vK + calc(hK+1, vK)
            v.append(q)

            return min(res1, res2)
        
        return calc(1, 1)
