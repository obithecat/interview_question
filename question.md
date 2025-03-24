面试题：限价订单簿重建与数据对齐

背景
在金融市场中，限价订单簿（Limit Order Book, LOB）是交易所用来记录所有买卖订单的数据结构。订单簿的动态变化由一系列事件（如新增订单、取消订单、成交等）驱动。你将从两个不同的数据流中获取数据：

    ​事件流：包含订单的增删改事件，用于重建订单簿。
    ​订单簿流：包含订单簿的快照数据，用于验证你重建的订单簿是否正确。

由于这两个数据流可能存在时间延迟（lag），你需要设计一种方法来对齐这两个数据流，以确保重建的订单簿与订单簿流一致。

任务
    ​重建限价订单簿：
        根据事件流数据，重建一个动态的限价订单簿。
        事件流的字段如下：

        ['Side', 'eventType', 'timeMs', 'Qty', 'Price', 'eventSeq', 'eventID', 'bidEventID', 'askEventID']
        
        eventID代表了这个事件的唯一确定ID。
        
        事件类型（eventType）可能包括：Limit,Market,BestPassive,Cancel,Trade
        你需要处理以下情况：
            订单（Limit/Market/BestPassive）: Limit是限价订单, Market是市价订单, BestPassive是本方passive最优价。
            取消订单（Cancel）：从订单簿中移除指定订单。
            成交（Trade）：bidEventID，askEventID分别代表这个交易买卖双方的eventID。

    ​数据对齐：
        
        订单簿流的字段如下：
        python

        ['BidPrice1', 'BidVolume1', 'BidPrice2', 'BidVolume2', 'BidPrice3', 'BidVolume3', 'BidPrice4', 'BidVolume4', 'BidPrice5', 'BidVolume5', 'AskPrice1', 'AskVolume1', 'AskPrice2', 'AskVolume2', 'AskPrice3', 'AskVolume3', 'AskPrice4', 'AskVolume4', 'AskPrice5', 'AskVolume5', 'timeMs']

        由于事件流和订单簿流可能存在时间延迟，你需要设计一种方法来对齐这两个数据流。
        你可以假设事件流和订单簿流的时间戳（timeMs）是单调递增的，但可能存在固定的或变化的延迟。

    ​验证：
        将你重建的订单簿与订单簿流进行对比，确保两者在时间对齐后的一致性。
        你需要输出重建的订单簿与订单簿流之间的差异，并解释可能的差异来源。

要求

    ​代码实现：
        使用Python编写代码，实现订单簿的重建和数据对齐。
        代码应具有良好的可读性和可维护性，包含必要的注释。

    ​对齐策略：
        描述你设计的数据对齐策略，并解释其合理性。
        你可以假设事件流和订单簿流的时间延迟是固定的，或者设计一种方法来动态估计延迟。

    ​测试与验证：
        使用提供的示例数据（或你自己生成的数据）进行测试。
        输出重建的订单簿与订单簿流之间的差异，并分析可能的误差来源。

提交内容

    ​代码文件：包含订单簿重建和数据对齐的Python代码。
    ​对齐策略说明：简要描述你设计的数据对齐策略。
    ​测试结果：输出重建的订单簿与订单簿流之间的差异，并分析可能的误差来源。

评估标准

    ​代码质量：代码的可读性、结构合理性和效率。
    ​对齐策略：策略的合理性和创新性。
    ​验证结果：对差异的分析是否准确和深入。
