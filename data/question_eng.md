Interview Question: Limit Order Book Reconstruction and Data Alignment

Background
In financial markets, the Limit Order Book (LOB) is a data structure used by exchanges to record all buy and sell orders. The dynamic changes in the order book are driven by a series of events (e.g., new orders, order cancellations, trades, etc.). You will receive data from two different data streams:

    ​Event Stream: Contains events for order additions, deletions, and modifications, used to reconstruct the order book.
    ​Order Book Stream: Contains snapshot data of the order book, used to validate the correctness of your reconstructed order book.

Due to potential time delays (lag) between these two data streams, you need to design a method to align them to ensure the reconstructed order book matches the order book stream.

Tasks

    ​Reconstruct the Limit Order Book:
        Reconstruct a dynamic limit order book based on the event stream data.
        The fields in the event stream are as follows:
        ['Side', 'eventType', 'timeMs', 'Qty', 'Price', 'eventSeq', 'eventID', 'bidEventID', 'askEventID']
            eventID uniquely identifies the event.
            Event types (eventType) include: Limit, Market, BestPassive, Cancel, Trade.
        Handle the following scenarios:
            ​Orders (Limit/Market/BestPassive):
                Limit: A limit order.
                Market: A market order.
                BestPassive: The best passive price on the same side.
            ​Cancel Order (Cancel): Remove the specified order from the order book.
            ​Trade (Trade): bidEventID and askEventID represent the eventIDs of the buyer and seller in the trade, respectively.

    ​Data Alignment:
        The fields in the order book stream are as follows:
        ['BidPrice1', 'BidVolume1', 'BidPrice2', 'BidVolume2', 'BidPrice3', 'BidVolume3', 'BidPrice4', 'BidVolume4', 'BidPrice5', 'BidVolume5', 'AskPrice1', 'AskVolume1', 'AskPrice2', 'AskVolume2', 'AskPrice3', 'AskVolume3', 'AskPrice4', 'AskVolume4', 'AskPrice5', 'AskVolume5', 'timeMs']
        Due to potential time delays between the event stream and the order book stream, design a method to align the two data streams.
        You can assume that the timestamps (timeMs) in both streams are monotonically increasing, but there may be fixed or varying delays.

    ​Validation:
        Compare your reconstructed order book with the order book stream to ensure consistency after time alignment.
        Output the differences between the reconstructed order book and the order book stream, and explain the possible sources of discrepancies.

Requirements

    ​Code Implementation:
        Use Python to implement the order book reconstruction and data alignment.
        The code should be readable, maintainable, and include necessary comments.

    ​Alignment Strategy:
        Describe the data alignment strategy you designed and explain its rationale.
        You can assume the time delay between the event stream and the order book stream is fixed, or design a method to dynamically estimate the delay.

    ​Testing and Validation:
        Test your implementation using the provided sample data (or data you generate).
        Output the differences between the reconstructed order book and the order book stream, and analyze the potential sources of errors.

Submission

    ​Code File: Python code for order book reconstruction and data alignment.
    ​Alignment Strategy Description: A brief explanation of your data alignment strategy.
    ​Test Results: Output the differences between the reconstructed order book and the order book stream, and analyze the potential sources of errors.

Evaluation Criteria

    ​Code Quality: Readability, structure, and efficiency of the code.
    ​Alignment Strategy: Rationality and innovation of the strategy.
    ​Validation Results: Accuracy and depth of the discrepancy analysis.
