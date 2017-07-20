---
layout: base
permalink: /note/2015-08-19-00
title: 【CheckiO】Determine the order
---

这题显然是个拓扑排序

不过用Python写拓扑排序实在是太麻烦了

后来看了一下高手的解法

    #!/usr/bin/env python2

    def checkio(data):
        distinct_letters = sorted(set("".join(data)))
        print distinct_letters
        #We just get couples of letters (a, b) such that a must be before b
        constraints = [(word[i], word[i + 1]) for word in data for i in range(len(word) - 1)]
        
        solution_found = False
        while not solution_found:
            solution_found = True
            for (a, b) in constraints:
                ia = distinct_letters.index(a)
                ib = distinct_letters.index(b)
                if ia > ib:
                    #We swap the letters
                    distinct_letters[ia] = b
                    distinct_letters[ib] = a
                    solution_found = False
        return "".join(distinct_letters)

发现自己的思路太僵化了

这毕竟不是ACM的题目

没有时间复杂度的限制

解决问题的时候完全可以采取一些时间复杂度高但容易实现的解法