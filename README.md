# find-the-minimum-and-maximum-numbevr-of-nodes-between-critical-point
class Solution {
    public int[] nodesBetweenCriticalPoints(ListNode head) {
        if (head == null || head.next == null || head.next.next == null) {
            return new int[]{-1, -1};
        }
        
        int firstCritical = -1;
        int lastCritical = -1;
        int minDistance = Integer.MAX_VALUE;
        int position = 1;
        int prevValue = head.val;
        head = head.next;
        
        while (head.next != null) {
            if ((head.val > prevValue && head.val > head.next.val) || 
                (head.val < prevValue && head.val < head.next.val)) {
                if (firstCritical == -1) {
                    firstCritical = position;
                } else {
                    minDistance = Math.min(minDistance, position - lastCritical);
                }
                lastCritical = position;
            }
            prevValue = head.val;
            head = head.next;
            position++;
        }
        
        if (firstCritical == lastCritical) {
            return new int[]{-1, -1};
        }
        
        return new int[]{minDistance, lastCritical - firstCritical};
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        
        // Example usage:
        ListNode node1 = new ListNode(1);
        ListNode node2 = new ListNode(3);
        ListNode node3 = new ListNode(2);
        ListNode node4 = new ListNode(2);
        ListNode node5 = new ListNode(5);
        ListNode node6 = new ListNode(1);
        ListNode node7 = new ListNode(2);

        node1.next = node2;
        node2.next = node3;
        node3.next = node4;
        node4.next = node5;
        node5.next = node6;
        node6.next = node7;

        int[] result = solution.nodesBetweenCriticalPoints(node1);
        System.out.println("Min Distance: " + result[0] + ", Max Distance: " + result[1]);
    }
}
