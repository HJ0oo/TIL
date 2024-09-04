# 1. 병합 정렬 (Merge Sort)
- 분할 정복 알고리즘 활용
  - top-down 방식. 자료를 최소단위까지 나눈 후에 차례대로 정렬해서 최종결과 얻음.
- 시간 복잡도 O(nlogn)
```py
def merge_sort(list_input):
    if len(list_input) == 1 : return list_input

    middle = len(list_input)//2
    left = list_input[:middle]
    right = list_input[middle:]

    left = merge_sort(left)
    right = merge_sort(right)
    
    return merge(left,right)


def merge(left_list, right_list):
    result = []
    while len(left_list) > 0 or len(right_list) > 0 :
        if len(left_list)>0 and len(right_list)>0 :
            if left_list[0] <= right_list[0] :
                result.append(left_list.pop(0))
            else :
                result.append(right_list.pop(0))
        elif len(left_list) > 0 :
            result.append(left_list.pop(0))
        elif len(right_list) > 0 :
            result.append(right_list.pop(0))
    return result

print(merge_sort([0,3,9,4,2,4,6,7,12,13,10]))
```