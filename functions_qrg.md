
## Functions Quick Reference Guide

### Confidence Intervals
Analyzing confidence intervals using bootstrapping and pandas GroupBy function:

    def calculate_statistic(sample):
        return sum(sample) / len(sample)
    
    def select_sample_with_replacement(data):
        length = len(data)
        try:
            return choices(data, k=length)
        except:
            return choices(data, k=10000)
    
    def bootstrapping_statistics(data):
        num_bootstraps = len(data)
        statistics = []
        data = data.tolist()
        for i in range(0,num_bootstraps+1):
            sample = select_sample_with_replacement(data)
            stat = calculate_statistic(sample)
            statistics.append(stat)
        ci_lower = np.percentile(statistics, 5)
        ci_upper = np.percentile(statistics, 95)
        return ci_lower, ci_upper

    ci = data.groupby(['categories'])['value'].agg([bootstrapping_statistics])


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU5NjYxMDIwNV19
-->