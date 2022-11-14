# viexpl - 临时测试版

针对一个数据视图（数据子集，由若干行列构成），（讨论输入视图到底是什么，是否包含聚合信息），使用预设的固定类型的洞察检测算子进行检测。最终生成视图对应在每个洞察类型上的显著性评分，和该洞察的一些具体的信息（如异常值、周期、和全局分布差异大的子分部等）


测试地址 https://gateway.kanaries.cn:2433/insight

## 接口
传入参数
```typescript
interface IStartSerive {
    dataSource: IRowp[];
    fields: IColumnp[];
    check_list: string[];（需要计算的洞察类型列表，默认为全部）
    breakdown: string[];（默认为区分度最大维度）
    aggrType: string;（默认为sum）
    subspaces: Array<IRowp[]>;（默认为最大子空间）
    rangeN: int;（默认为5）
}
```
返回
```typescript
interface IStartReturns {
    success: boolean;
    data: Array<insightTypes: （insightTypes为洞察类型，与check_list输入对应）
        {
            'score':score,
            'para':
            {
                para（画图相关参数）
                'explain':string;(描述文本)
            }
        }>
}
```

## 洞察类型整理
解读.png![图片](https://user-images.githubusercontent.com/8137814/201577294-446bd2b1-69ee-4193-8725-690f1217dd9a.png)

## 参考文献
参考资料
[1] Tang, Bo, et al. "Extracting top-k insights from multi-dimensional data." Proceedings of the 2017 ACM International Conference on Management of Data. 2017.
[2] Ding, Rui, et al. "Quickinsights: Quick and automatic discovery of insights from multi-dimensional data." Proceedings of the 2019 International Conference on Management of Data. 2019.
[3] Mihart, Maggies, MSFTmgblythe. 2021. Types of insights supported by Power BI. Accessed at https://docs.microsoft.com/en-us/power-bi/consumer/end-user-insight-types
[4] T. Sellam, E. Müller and M. Kersten, "Semi-automated exploration of data warehouses," in 2015, . DOI: 10.1145/2806416.2806538.
[5] Ma, Pingchuan, et al. "MetaInsight: Automatic Discovery of Structured Knowledge for Exploratory Data Analysis." Proceedings of the 2021 International Conference on Management of Data. 2021.
[6] Saket, Bahador, Alex Endert, and Çağatay Demiralp. "Task-based effectiveness of basic visualizations." IEEE transactions on visualization and computer graphics 25.7 (2018): 2505-2512.
[7] Amar, Robert, James Eagan, and John Stasko. "Low-level components of analytic activity in information visualization." IEEE Symposium on Information Visualization, 2005. INFOVIS 2005.. IEEE, 2005.

## Milestones
- [x] 可行性验证
- [x] baseline方案实现
- [ ] 工程优化
  - [x] 并发量可扩展性
  - [ ] 维护Session，避免反复传输&解析
  - [ ] websocket实现session
- [ ] 可解释性优化
- [ ] 评分机制优化
