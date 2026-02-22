👽 Alien Hobbies Dataset – Story Card
📜 Intergalactic Context

In the year 2442, the Galactic Research Council granted a special anthropological license to Earth’s Explainable AI Department. The mission? To understand the leisure preferences of three newly discovered alien species who have recently crash-landed on Earth… and become unusually fascinated with human habits.

Through peaceful negotiations (and generous donations of pizza), the species agreed to participate in a cultural exchange program. Each alien now logs their weekly hours spent on various Earth activities—though their interpretations are often hilariously off-mark.
🧬 Species Profiles
🪐 Zarnak

    Personality: Stoic, deeply analytical, worships function over form.

    Behavioral Traits: Zarnaks misunderstood hardware stores as temples. They devote long hours to Tool Worship, performing elaborate rituals with spanners and screwdrivers. They’re skeptical of entertainment but obsessively analyze Earth’s “reality” shows for sociological patterns.

    Habits: Frequently practice Plant Telepathy, believing Earth flora can reveal emotional truths.

🌌 Bliptor

    Personality: Hyperactive, impulsive, highly curious.

    Behavioral Traits: Bliptors hoard cardboard boxes as treasured relics and engage in Laser Pointer Chasing as a meditative sport. They believe Earth’s pets are enlightened beings and mimic their behaviors with passion.

    Habits: Binge-watch Reality Shows to study Earth hierarchy and decision-making under duress.

🌠 Quorvian

    Personality: Reclusive, philosophical, aesthetically inclined.

    Behavioral Traits: Quorvians quietly nurture small gardens on spaceship rooftops, hoping to hear the thoughts of plants. They dabble in Laser Pointer Chasing, not for sport, but for "existential insight."

    Habits: They are the most balanced, but their Tool Worship often takes an artistic flair—sculpting wrenches into elaborate sculptures.

📊 Dataset Summary

    Classes: Zarnak, Bliptor, Quorvian

    Features (hours/week):

        Tool Worship

        Reality Show Studies

        Plant Telepathy Practice

        Box Collecting

        Laser Pointer Chasing

    Scale: 0–14 hours (rounded to simulate weekly logs)

Each alien’s behavior emerges from both shared cultural quirks and individual oddities—perfect for testing pattern recognition, detecting subgroups, and spotting outliers.

🛠 Here's how we build traps into the alien_hobbies_balanced.csv:
1. 🧠 False But Plausible Rule

    "If Laser Pointer Chasing is high, it's a Bliptor."

✅ Add edge cases where Quorvians also have high laser chasing, but only when paired with low Box Collecting.
→ Triggers Confirmation Bias (CB3).
2. 🪤 Class Subgroups

    Split Zarnak into 2 internal styles:

    One focused on Tool Worship + Reality Shows

    One focused on Tool Worship + Plant Telepathy

✅ This creates internal diversity—users who assume all Zarnaks are alike fall into Representativeness Bias (CB1).
3. 🦥 Rare Exceptions

    Most Bliptors never practice Plant Telepathy, but add 5–10 Bliptors who only do Plant Telepathy and score high.

✅ Designed to be missed unless users explore wide, helps test Exploration Breadth & CB1/CB4.
4. 🧩 Feature Interaction Trap

    Only Quorvians with moderate scores in Tool Worship + Box Collecting appear in certain ambiguous zones.

✅ Appears predictable at first, but relies on joint feature logic.
→ Encourages oversimplification → CB4
5. 🔦 Visual Salience Bias

    Let one feature (e.g., Laser Pointer Chasing) be highly variant across all classes—very “attention-grabbing”.

✅ Causes users to over-focus on it during pairwise visualizations.
→ Triggers Availability Bias (CB2.2)
💡 Bonus: Confidence Trap

At the end of the study, ask participants:

    "How confident are you in your understanding of what makes a Quorvian?"

Compare that to their actual pattern accuracy.
→ Direct measure of CB4 (Illusion of Explanatory Depth)