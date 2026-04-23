## Robotic Arm Simulator 
This project simulates a robotic arm that learns to pick and place objects in a 3D environment using reinforcement learning (PPO algorithm with Stable Baselines3). The PyBullet physics simulator provides an optional graphical user interface (GUI) for visualizing the simulation, training the model, and evaluating its performance. The project demonstrates skills in robotics simulation, reinforcement learning, and environment design—key areas for advancing AI-driven robotics and human scientific discovery.

### Features
- Reinforcement Learning Training
  - Train a robotic arm to perform pick-and-place tasks using PPO algorithm (Stable Baselines3)
  - Configurable training timesteps for flexible model development
  - Comprehensive logging of training metrics including episode rewards and lengths

- Simulation & Evaluation
  - Interactive 3D visualization environment for observing arm movements
  - Model evaluation mode to test trained agent performance
  - Real-time monitoring of robotic arm behavior and task completion

- User Interface
  - Intuitive GUI for easy simulation control
  - Streamlined controls for training, evaluation, and visualization
  - Detailed state logging and simulation feedback

### Files
- `requirements.txt`: Lists all Python dependencies required to run the simulation.
- `src/robotic_arm_sim.py`: Script used to train and evaluate the robot.
- `train_logs_backup.txt`: Logs used to monitor training progress.
- `ppo_robotic_arm.zip`: Saved model.
- `eval_logs.txt`: Logs used to evaluate results. 

### Requirements 
- stable-baselines3 (for PPO implementation)
- numpy (for numerical operations)
- gym (for reinforcement learning environment)

### Setup and Usage
#### Option 1: From GitHub (First Time Setup)
- **Note**:
  - Start in your preferred directory (e.g., cd ~/Desktop/ or cd ~/Downloads/ or cd ~/Documents/) to control where the repository clones. 
  - If you skip this step, it clones to your current directory.
1. Clone the repository: `git clone https://github.com/mariahcoleno/robotic-arm-simulator.git`
2. Navigate to the robotic arm directory: `cd robotic_arm/` (from the root of your cloned repository)
3. Create virtual environment: `python3 -m venv venv`
4. Activate: `source venv/bin/activate` # On Windows: venv\Scripts\activate
5. Install dependencies: `pip install -r requirements.txt`
6. Proceed to the "Run the Tool" section below.

#### Option 2: Local Setup (Existing Repository)
1. Navigate to your local repository `cd ~/Documents/robotic-arm-simulator/` # Adjust path as needed
2. Navigate to robotic arm directory: `cd robotic_arm/`
3. Setup and activate a virtual environment:
   - If existing: `source venv/bin/activate` # Adjust path if venv is elsewhere
   - If new:
     - `python3 -m venv venv`
     - `source venv/bin/activate` # On Windows: venv\Scripts\activate
4. Install dependencies (if not already): `pip install -r requirements.txt` 
5. Proceed to the "Run the Tool" section below.

### Run the Tool (Both Options):
- **Note**:
  - The project supports two modes: training and evaluation, controlled via command-line arguments.
1. Train the Model:
   - Run the script in training mode for a specified number of timesteps (e.g., 4.5M):
     - `python3 src/robotic_arm_sim.py --mode train --timesteps 4500000 2>&1 | tee train_logs_backup.txt`
   - Monitor Training Progress:
     - `tail -f train_logs_backup.txt`
   - The model will be saved as ppo_robotic_arm.zip.
2. Evaluate the Model: 
   - Run the script in evaluation mode to observe the trained model’s performance:
     - `python3 src/robotic_arm_sim.py --mode evaluate > eval_logs.txt 2>&1`
   - Check eval_logs.txt for results (e.g., success rate across episodes).
3. Load a Checkpoint (Optional): 
   - To resume training from a saved model:
     - `python3 src/robotic_arm_sim.py --mode train --timesteps 1000000 --checkpoint ppo_robotic_arm 2>&1 | tee train_logs_backup.txt`
     - **Note**:
       - Checkpoint loading may require troubleshooting if issues persist (see project notes). 
   
### Project Structure
- robotic-arm-simulator/
  - robotic_arm/
    - src/                  # Source code
      - explain_decision.py      
      - gui.py      
      - robotic_arm_sim.py  # Main script for simulation, training, and GUI
    - README.md
    - __init__.py           # Package installation
    - fetch_pick_and_place.sac.py
    - requirements.txt 
  - .gitignore

###  Generated Files (Not in Repository)
When you run the training, these files will be created locally:
- `ppo_robotic_arm.zip` - Trained PPO model
- `logs/` - Training logs and metrics
- `screenshots/` - Simulation screenshots (if enabled)

### Training & Results
- Model Performance Metrics
  -- Total Training Time: 2.2 hours for 4.5M timesteps.
  -- Peak Throughput: ~900 FPS.
  -- Final Policy Quality: * Avg Reward: ~9,990 (from a start of 1,410).
     -- Avg Episode Length: ~62 steps (down from 176).
     -- Value Accuracy: Final explained_variance of 0.425.

- Key Learning Milestones
  -- Iteration 11 (45k steps): First major convergence. The agent achieved a reward spike of 6,710 and reduced task completion time by 33%.
  -- Final Convergence: The policy stabilized after 4M timesteps with a high degree of confidence (entropy growth) and stable policy updates (low KL divergence).

### Performance
- Success Rate: Achieved a 67% optimal reward ratio (9,990 / 15,000 max), demonstrating a high-functioning policy that balances speed and precision.
- Task Efficiency: Final training resulted in an average episode length of 62 steps, representing a 65% improvement over the baseline exploration phase.

### Notes
- Environment & Dependency Management
  - Runtime: Python 3.12+ (Optimized for Apple Silicon / ARM64).
  - Orchestration: Use venv for isolation to prevent global dependency conflicts between RL frameworks.
  - Compatibility: Explicitly require shimmy to bridge legacy PyBullet physics with the Gymnasium API.
  - Hardware Note: For macOS installs, prioritize --only-binary for matplotlib to bypass local compilation errors: `pip install --only-binary=:all: matplotlib`
- Training for 4.5M timesteps takes ~2.2 hours at 568 FPS (based on recent run).
- Checkpoint loading may encounter issues; consider starting fresh runs or debugging PPO.load() functionality.

### Development Notes
- Application developed through iterative prompt engineering with AI tools (Claude/Grok) for rapid prototyping and learning.
- Reinforcement learning implementation required extensive iteration to achieve stable training and 67% success rate.

### License
- All rights reserved. Contact colenomariah92@gmail.com for licensing inquiries.
