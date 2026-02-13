
TRM Based RAG Tool Selector
- https://github.com/waddadaa/gpagent?tab=readme-ov-file


## Abstract

- a sequence of States => a sequence of Actions mapping
	- Order, item1, item2 => check balance, order, and so on


## Concrete Ideas

- Supply Chain & Warehouse "Slotting" Logic
	- How we can do? :https://www.penskelogistics.com/solutions/warehousing-and-distribution/warehouse-design/maximize-warehouse-space/
	- Dataset: https://www.kaggle.com/datasets/aikinomichi/mega-star-distribution-centre
		- Dataset Analysis: https://www.kaggle.com/code/aikinomichi/mega-star-distribution-centre-inventory-analysis
	- Amazon Dataset: https://github.com/nisarg14/CSE523-Machine-Learning-Gophers

## Optimization (Traveling Sale Person)

### How to Prototype This

To build a "Less is More" style prototype for this Saint-Gobain use case, you would:

1. **Gridify the Map:** Convert the coordinates of the Saint-Gobain sites into a 2D matrix. 
2. **Define the "Colors":** * 
	- `0`: Empty space
    - `1`: Site needing inspection
    - `2`: Inspector A
    - `3`: Inspector B
3. **The Goal State:** A grid where all `1`s have been visited by a `2` or `3` in the shortest sequence of steps without any inspector exceeding their "move limit."

This is essentially a **Grid-based Scheduling Engine**. It moves away from "predicting text" and toward "solving the puzzle of efficiency."

## Dataset
 - 