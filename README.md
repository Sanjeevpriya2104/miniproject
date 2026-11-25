<<<<<<< HEAD
# AI-Augmented Edge Resource Management for Smart Cities

Mini Project – Dharshini S (212224040074), B.E. CSE, Saveetha Engineering College

This is a working prototype of the system designed in the Review 1 and Review 2 reports. It has:
- a Python simulation of 5 smart-city edge nodes
- a Q-learning (reinforcement learning) task allocator
- four baseline policies to compare against
- a web dashboard

---

## 1. Requirements
- Python 3.9 or newer
- VS Code with the **Python** extension (by Microsoft)
- No internet needed after installing Flask (Chart.js is bundled locally)

## 2. Run in VS Code (step by step)

1. Extract the zip, then in VS Code use **File → Open Folder → `edge-resource-manager`**.
2. Open a terminal: **Terminal → New Terminal**.
3. Create a virtual environment (optional, but recommended):
   ```bash
   python -m venv venv
   # Windows:
   venv\Scripts\activate
   # Linux / macOS:
   source venv/bin/activate
   ```
4. Install Flask:
   ```bash
   pip install -r requirements.txt
   ```
5. Start the app:
   ```bash
   python app.py
   ```
6. Open **http://127.0.0.1:5000** in your browser.

To stop the server, press `Ctrl + C` in the terminal.

You can also press **F5** in VS Code and choose **"Run Edge Resource Manager (Flask)"**.

## 3. Run the test cases (TC01 – TC07)
```bash
python -m unittest discover tests -v
```
You can also open the **Test Cases** page in the web app and click **Run all tests**. It fills in the "Actual Result" and "Pass/Fail" columns of Tables 7.3.1 and 7.3.2.

---

## 4. Web pages

| Page | What it shows |
|---|---|
| **Live Dashboard** | Real-time city simulation: node CPU, memory, queue, latency and power, live charts, recent decisions and events. You can change the policy, the load, the rush-hour burst, and turn AI learning on or off. |
| **Submit Task** | Send one request (traffic / surveillance / emergency / environment) and see the evaluation of every node: eligibility, estimated completion time, whether it meets the deadline, and its Q-score. You can also take a node offline or make it send missing values. |
| **Policy Comparison** | Runs all 5 policies on the same workload. Shows a results table, completion time, deadline success, energy, node utilisation, per-application success and a timeline. CSV decision logs can be downloaded. |
| **Train AI Agent** | Retrains the Q-learning agent and shows the learning curve. The trained table is saved to `models/q_table.json`. |
| **Test Cases** | TC01–TC07 from Chapter 7. |
| **Decision Log** | The Performance Reporter's record of every decision. |
| **About Project** | Architecture, infrastructure, workloads and policies. |

## 5. Screenshots for Appendix 2 (Sample Output)
1. Live Dashboard: click **Start** and wait about 15 s.
2. Submit Task: click **🚑 Emergency** and then **💾 128 GB task**.
3. Policy Comparison: click **Run comparison**.
4. Train AI Agent: click **Train agent**.
5. Test Cases: click **Run all tests**.

---

## 6. Project structure (matches Chapter 6 modules)
```
edge-resource-manager/
├── app.py                  # Flask web server + REST API
├── edge/
│   ├── models.py           # Task, EdgeNode, ResourceSnapshot (ER diagram entities)
│   ├── monitor.py          # Module 1 – Resource Monitoring (stale / missing detection)
│   ├── allocator.py        # Module 2 – AI allocation (Q-learning) + baseline policies
│   ├── balancer.py         # Module 3 – Load balancing (sustained-overload detection)
│   ├── reporter.py         # Module 4 – Performance reporting & metrics
│   ├── simulation.py       # Workload generator, training, policy comparison
│   └── testcases.py        # TC01–TC07
├── templates/index.html    # Web page
├── static/css/style.css
├── static/js/app.js        # Front-end logic
├── static/js/chart.umd.min.js  # Chart.js (bundled, works offline)
├── models/q_table.json     # Trained Q-table (auto-created on first run)
├── tests/test_system.py    # unittest runner
└── requirements.txt
```

## 7. How the AI allocator decides (Section 5.2.1)
1. Read the latest snapshots. Stale or missing nodes are excluded.
2. Remove nodes without enough memory or bandwidth. If no node is left, the task is **deferred with a capacity warning**.
3. Remove nodes in **sustained overload** (as long as at least one other node is left).
4. Prefer nodes predicted to meet the deadline. The prediction is network latency + transfer time + queue wait + processing time.
5. Choose the node with the highest **Q-value**:
   - state = task type, node, queue-delay bucket, deadline feasibility
   - reward = deadline success, completion time, energy and overload, weighted by priority
6. If the learning policy is disabled, the **least-loaded fallback** is used and the event is logged.

The nodes have random run-time slow-downs that the planner cannot see, so the agent learns from the actual outcomes which nodes are reliable.

At normal load, the AI groups most work on N5, the fastest and most energy-efficient node. At higher loads (Load 2–3×) it spreads work to the other nodes.

**Note:** Energy figures are *model-based estimates* (linear idle-to-max power model), not hardware measurements. The whole system is a simulation, not a real city deployment.
=======
# edge-management

