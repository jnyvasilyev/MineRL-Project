# MineRL-Project

This repo is for archival purposes. Original project submission is https://github.com/laithaustin/mine_agent_baselines

## Installation Guide
First make sure to have all of the needed requirements using our requirements.txt file.
```pip install -r requirements.txt```

You will likely encounter an issue with the installation of MineRL if you are on MacOS or windows. In order to circumvent this follow these instructions:

0. First follow install instructions on the official MineRL docs website
https://minerl.readthedocs.io/en/v0.4.4/tutorials/index.html

1. Install the follwing MixinGradle file that is missing from the repo's cache in order for Malmo to work:
https://drive.google.com/file/d/1z9i21_GQrewE0zIgrpHY5kKMZ5IzDt6U/view?usp=drive_link

2. Clone the mineRL repo locally and checkout their v0.4 branch that we are using.
```git clone https://github.com/minerllabs/minerl.git```
```cd minerl```
```git checkout v0.4```

3. Go into the build.gradle file
```cd minerl/Malmo/Minecraft```

4. Then update the build.gradle in the following way:

4.1 Add the following to the repositories section:
```
maven {
    url 'your path to the parent directory of the mixingradle file you installed'
}
```

4.2 Make sure your dependencies section looks like this:
```
dependencies {
        classpath 'org.ow2.asm:asm:6.0'
          classpath('MixinGradle-dcfaf61:MixinGradle:dcfaf61'){ // 0.6
            // Because forgegradle requires 6.0 (not -debug-all) while mixingradle depends on 5.0
            // and putting mixin right here will place it before forge in the class loader
            exclude group: 'org.ow2.asm', module: 'asm-debug-all'
        }

        classpath 'com.github.brandonhoughton:ForgeGradle:FG_2.2_patched-SNAPSHOT'
    }
```

5. Now you should be able to pip install using this directory and have no issues.

## Files:

### Navigate Environment Files
**ppo_bc_navigate.zip** - Full BC+PPO model for navigate task  

**student_ppo_policy_navigate** - Pretrained policy weights using BC for navigate task  

**student_ppo_navigate** - Model from which pretrained policy was taken, SB3 needs this when loading policy  

**navigate_bc.py** - Change file paths in config and DATA global var at beginning of file accordingly to run the following:  

	def main():

    		# Trains BC policy using supervised learning
    		#train_bc()

    		# rl_bc = True if you want to continue training BC policy with RL
    		# rl_bc = False if you want just RL
    		#train_rl(rl_bc=True)

    		# bc_only = True if you want to test just the BC policy
    		# bc_only = False if you want to test an RL model
    		test(bc_only=False)

### Treechop Environment Files
**ppo_bc_treechop.zip** - Full BC+PPO model for treechop task  

**student_ppo_policy_treechop** - Pretrained policy weights using BC for treechop task  

**student_ppo_treechop** - Model from which pretrained policy was taken, SB3 needs this when loading policy  


**navigate_bc.py** - Change file paths in config and DATA global var at beginning of file accordingly to run the following:

	def main():

    		# Trains BC policy using supervised learning
    		#train_bc()

    		# rl_bc = True if you want to continue training BC policy with RL
    		# rl_bc = False if you want just RL
    		#train_rl(rl_bc=True)

    		# bc_only = True if you want to test just the BC policy
    		# bc_only = False if you want to test an RL model
    		test(bc_only=False)
