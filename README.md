# leetcode-----2901
Longest Unequal Adjacent Groups Subsequence II
//code in java
import java.util.*;

public class Solution {
    public List<String> getWordsInLongestSubsequence(String[] words, int[] groups) {
        int n = words.length; // Calculate n from the length of words array
        int[] dp = new int[n];
        int[] prev = new int[n];
        Arrays.fill(dp, 1);
        Arrays.fill(prev, -1);

        for (int i = 1; i < n; ++i) {
            for (int j = 0; j < i; ++j) {
                if (groups[i] == groups[j]) continue;
                if (words[i].length() != words[j].length()) continue;
                if (hammingDistance(words[i], words[j]) != 1) continue;
                if (dp[i] < dp[j] + 1) {
                    dp[i] = dp[j] + 1;
                    prev[i] = j;
                }
            }
        }

        // Find the index of the maximum value in dp
        int maxIndex = 0;
        for (int i = 1; i < n; ++i) {
            if (dp[i] > dp[maxIndex]) {
                maxIndex = i;
            }
        }

        // Reconstruct the subsequence
        LinkedList<String> result = new LinkedList<>();
        int index = maxIndex;
        while (index != -1) {
            result.addFirst(words[index]);
            index = prev[index];
        }

        return result;
    }

    private int hammingDistance(String s1, String s2) {
        int dist = 0;
        for (int i = 0; i < s1.length(); ++i) {
            if (s1.charAt(i) != s2.charAt(i)) {
                ++dist;
            }
        }
        return dist;
    }
}
