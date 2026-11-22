1.  In the project you developed further, what did a fresh session get wrong or ask about that an earlier round had already settled? What was missing from the repository that would have prevented it?

    One rule in my CLAUDE.md stated that commits were to be done by the me (I wanted to do commits manually for a little bit before letting my agents do them). Whenever I would paste the start-of-round-prompt, the agent would always point out that there was a conflict between the no commits rule and sentence in the prompt (number 2 in the start-of-round prompt, for example). For every round after round 2, a new rule would end up in the CLAUDE.md file that would act as an exception to the no commit rule (I deleted them each time they were added). If I had added a file containing the start-of-round prompt (with a couple of changes to it), I would have prevented Claude from creating an exception to the no rule commit.

2.  In the round that changed an earlier requirement, what broke? Did the tests catch it, and does the decision record explain the change to someone who was not there?

    In round 6, I added an animation to a screen and changed an exisiting feature from round 5 (white boxes behind selected options -> brackets surrounding the selected option). Nothing broke, but the original animation would break, so I simplified it a couple of times until it worked. For some reason, when I did my first commit to problem.md for round 6 (commit cd3a810), I never included the requirement stating the change. I ended up adding it after the handoff file for round 6 was created. An ADR file for it was created (decisions/0013-brackets-instead-of-white-box). Also, lines 133-145 in history.md document how the change was implemented (last section of the entire file).

3.  Name one test that caught a real problem, or one test the assistant wrote that checked nothing useful. Quote it.

    Even though the tests are all named with what they actually test, its still not enough for me to determine what tests are useful/useless. So, I had claude summarize what each test does. I chose this test:

    def test_R1_1_correct_space(self): ---> found inside test_logic.py starting on line 51
    t = logic.TypingTest("a b")
    t.type_char("a")
    t.type_char(" ")
    self.assertEqual(t.status(1), logic.CORRECT)

    This test makes sure that spaces return "CORRECT" when they are typed in. There is no special case in my program for spaces (like a double space to represent newlines as these are ignored), and if there was, then this test would fail. Thus, this test is redundant.

4.  Choose one commit you would now write differently, and say how.

    Any commit related to updating history.md, like commit 055acbc (updated history.md with the user/agent conversation for R3). The only thing inside histpry.md is a log of conversations between me and user for each round, so I don't have to say thats whats inside each commit, just what I did and why. I would rewrite these commits like this:

        git commit -m "updated history.md for Round 3"

5.  Choose one function in the project you developed further that you did not read while building it. Without an assistant open, read it and write what you think it does, in two or three sentences. Then ask an assistant, and say what you got right and wrong.

    def \_on_screen(cells, screen_cols, screen_rows):
    return [c for c in cells if 0 <= c.row < screen_rows and 0 <= c.col < screen_cols]

    This was one of the few functions without comments describing what it does. I think its a check to make sure if a certain frame on screen is actually in the screen. If a cell falls between 0 and screen_rows -1 (inclusive) and between 0 and screen_cols - 1 (inclusive), then return true and couint it as a frame.

    What I got right: I correctly said this function is a check.
    What I got wrong: Its checking cells, not frames (cells are like pixels), and the return type is not a boolean but a list (a list of pixels that fall on the screen).
