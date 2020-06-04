<!DOCTYPE html>
<html lang="en" class="no-js">
    <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>UM5R Origin Generator</title>
    <meta name="description" content="Ultramodern5 Redux Life Event Generator.">
    <meta name="keywords" content="UM5R, Utility">
    
    <!-- Android Lolipop Theme Color -->
    <meta name="theme-color" content="#141414">

    <!-- Fonts -->
    <link href="https://fonts.googleapis.com/css?family=Titillium+Web:300,400,700" rel="stylesheet">
</head>
    <body>
                <h2 id="ultramodern5-redux-origin-generator">Ultramodern5 Redux Life Event Generator</h2>

<div style="width:90%;padding:20px;">
<style type="text/css">
button {
    padding: 0;
    background: transparent;
    font-size: inherit;
    border: 0;
    outline: 0;
}

.buttonR {
    -webkit-transition-duration: 0.4s;
    transition-duration: 0.4s;
    background-color: #993300;
    color: white;
    padding: 6px; 
    /* border: 2px solid black; */
    font-size: 16px;
}

.buttonR:hover {
    background-color: #CC6600;
    color: white;
    /* padding: 3px; */ 
    /* border: 2px solid black; */
}

.Divbuttons {
    /* float:left; */
    margin: auto;
    padding: 3px;
    /* border: 2px solid black; */
    display: inline-block;
}

.divsub {
    margin: 3px;
    border: 2px solid #993300; /* border: 2px #0099CC solid; */
    text-align: left; 
    vertical-align: top; 
    padding: 3px; 
    display: inline-block;
    width: 99%;
    /* height: 400px; */
    overflow: auto;
}

h2.ds {
    margin: 1rem 0 1rem;
    font-size: 2.0rem;
    line-height: 1.2;
    color: #CC6600; /* #0768C9; */
}

.tabs {
    /* display: inline-block; */
    display: flex;
    flex-wrap: wrap; /* make sure it wraps */
}

.tabs label {
    order: 1; /* Put the labels first */
    display: block;
    padding: 1rem 2rem;
    margin-right: 0.2rem;
    cursor: pointer;
    color: white;
    background: #993300; /* #90CAF9; */
    font-weight: bold;
    transition: background ease 0.2s;
}

.tabs .tab {
    order: 99; /* order: 99; Put the tabs last */
    flex-grow: 1;
    width: 100%;
    display: none;
    padding: 6px; /* padding: 1rem; */
    background: #CCCC99; /* #fff; */
}

.tabs input[type="radio"] {
    display: none;
}

.tabs input[type="radio"]:checked + label {
    background: #CC6600; /* #fff; */
}

.tabs input[type="radio"]:checked + label + .tab {
        display: inline-block; /* display: block; */
}

@media (max-width: 45em) {
    .tabs .tab, .tabs label {
        order: initial;
    }
    .tabs label {
        width: 100%;
        margin-right: 0;
        margin-top: 0.2rem;
    }
}

.Rsalvage {
    float:left;
    padding:10px;
    border: 2px solid black;
}
</style>

<div class="tabs">
<input type="radio" name="tabs" id="tabone" checked="checked" />
<label for="tabone">Lifepaths</label>
<div class="tab">

<div id="xbuttons" class="Divbuttons">
<button class="button buttonR" onclick="buttonGenerate();">Generate Normal Lifepath</button>
<button class="button buttonR" onclick="buttonGenerate(true);">Generate Apex Lifepath</button>
</div>

</div>
<input type="radio" name="tabs" id="tabtwo" />
<label for="tabtwo">Human Genetics</label>
<div class="tab">

<div id="xbuttons" class="Divbuttons">
<button class="button buttonR" onclick="buttonGeneticBenefit();">Genetic Benefit</button>
<button class="button buttonR" onclick="buttonShortComings();">Shortcomings</button>
</div>

</div>
</div>

<br style="clear:both;" />
<div id="origindata" class="divsub" style="order: 100;flex-grow: 1;"><div id="origin">
Please select a button above.<br/>
<br/>
This is the one thing you cannot choose, where you must gamble the events of your life. After selecting your current age, generate your origin. The final result is the number of life-changing events which occurred in your past, in the order in which they are rolled. You can spread the events around as much as you'd like, and they can even be swapped around if it best suits the backstory the GM is approving.<br/>
<br/>
You can assume each event marks one year of your life. If older, each event could occur every few years. If younger, the events could occur over a matter of a few months.
</div></div>
<br /><br />

<script type="text/javascript">
// ////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Utility functions below /////////////////////////////////////////////////////////////////////////
// ////////////////////////////////////////////////////////////////////////////////////////////////////////////

function rolldice(min, max) {

    // min (included) and max (excluded)
    // Math.floor(Math.random() * (max - min + 1) ) + min;
    var rDice = Math.floor(Math.random() * (max - min + 1) ) + min;
    return rDice
}

function numFormat(x){
  return x.toLocaleString('en-IN');
}

// ////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Lifepath below /////////////////////////////////////////////////////////////////////////////////////
// ////////////////////////////////////////////////////////////////////////////////////////////////////////////

function parenting() {
 var a1 = [
            'Both parents are alive.',
            'Orphan – Your parents are dead.',
            'Abandoned – Your parents are gone, but unlikely dead.',
            'One parent is absent',
            'Original parents divorced, and your guardian (Mother) remarried',
            'Original parents divorced, and your guardian (Father) remarried',
          ];

    var dData = '';
    var dRoll = rolldice(1, 20);

    switch(true) {
        case (dRoll <= 11):
            dData += a1[0];
            dData += '<ul><li>[Status] ' + status() + '</li></ul>';
        break;

        case ((dRoll >= 12) && (dRoll <= 14)):
            dData += a1[1];
            dData += '<ul><li>[Casualty] ' + casualty() + '</li>';
            dData += '<li>[Surrogate] ' + surrogate() + '</li></ul>';
        break; 

        case ((dRoll >= 15) && (dRoll <= 17)):
            dData += a1[2];
            dData += '<ul><li>[Separation] ' + separation() + '</li>';
            dData += '<li>[Surrogate] ' + surrogate() + '</li></ul>';
        break; 

        case ((dRoll >= 18) && (dRoll <= 20)):
            dData += a1[3];
            var dRoll = rolldice(1, 20);
                if(dRoll <= 10) {
                    dData += ' (Mother). <ul>';
                } else {
                    dData += ' (Father). <ul>';
                }

            var dRoll = rolldice(1, 20);
                if(dRoll <= 10) {
                    dData += '<li>[Casualty] ' + casualty() + '</li>';
                } else {
                    dData += '<li>[Separation] ' + separation() + '</li>';
                }

            dData += '<li>[Status] ' + status() + '</li></ul>';
        break; 
    }

    return dData;
}

function status() {
 var a2 = [
            'Your family has had its highs and lows, but you\’ve got nothing to complain about.',
            'A bad business deal bankrupted the estate—you\’ve got nothing.',
            'A parent or parents were abusive; you hated them.',
            'Your family got swept up in a cult.',
            'Parents doted on either you or a sibling hand and foot at the expense of others. There might be resentment.',
            'Unpredictable employment moved your family from town to town, never establishing roots.', 
            'You lived a bucolic life (on a farm, off the grid).',
            'Your family is a cog in a well-oiled corporate or government machine.',
            'Your family sold you into slavery—whether out of selfishness or extreme need, makes no difference to you.',
            'Trauma tore the family apart and you\’ve never fully recovered.',
            'The family would be better off without you. You are damaged.',
            'Your parents are criminals, and that\’s the source of some stress. You don\’t need to follow in their footsteps.',
            'Your family is embroiled in a rebellion. It\’s respectable, but also dangerous.',
            'You are the child of a military family. Your family moved around a lot.',
            'Your family is really close; you call each other at least once a week.'
          ];
    var dRoll = rolldice(0, (a2.length - 1));

    return a2[dRoll];
}

function casualty() {
 var a3 = [
            'Died under mysterious circumstances. No one knows what killed them.',
            'Murdered in a targeted attack (it was not random violence).',
            'Murdered by gang violence.',
            'Assassinated by a corporation/organization.',
            'Assassinated by the government/kingdom.',
            'Killed in a terrorist strike—he/she was not a target, but the location was.', 
            'Died by natural causes. (cancer, diabetes, etc.).',
            'Died in a viral outbreak.',
            'Suicide—you could deny it, but it\’s the truth.',
            'Killed in an accident (fire, vehicle crash, drowning, etc.).',
            'Casualty of armed conflict.',
            'Casualty of a natural disaster (earthquake, tornado, flood, etc).'
          ];
    var dRoll = rolldice(0, (a3.length - 1));

    return a3[dRoll];
}

function separation() {
 var a4 = [
            'Amnesia—the memories of you are gone.',
            'In hiding, probably to protect you.',
            'Confinement (jail, concentration camp).',
            'Vanished, just like that.',
            'Kidnapped, you\’re certain of it.',
            'Separation, for your safety or someone else\’s.',
            'There were psychological problems in place. Maybe they were committed.',
			'Deported to another country.'
          ];
    var dRoll = rolldice(0, (a4.length - 1));

    return a4[dRoll];
}

function surrogate() {
 var a5 = [
            'You were raised by relatives.',
            'You were raised by relatives.',
            'You were adopted.',
            'You bounced through foster homes.',
            'You were reared on the streets (gang).',
            'You joined a cult or monastery.',
            'You were raised in an orphanage.',
            'An inheritance paid for a private school.',
            'You joined a military organization.',
            'Your family is atypical; you were raised by ' + surrogateAtypical() + '.'
          ];
    var dData = '';
    var dRoll = rolldice(0, (a5.length - 1));

    if(dRoll <= 2) {
        dData += a5[dRoll] + ' <ul><li>[Surrogate Parenting] ' + parenting() + '</li></ul>';
    } else {
        dData = a5[dRoll];
    }

    return dData;
}

function surrogateAtypical() {
 var a51 = [
            'Apes.',
            'Wolves.',
            'Robots.',
            'Aliens.',
            'Government Researchers.',
            'Mountain Folk.',
            'A corporate enclave.',
			'A cult of religous fanatics.'
          ];
    var dRoll = rolldice(0, (a51.length - 1));

    return a51[dRoll];
}

function siblings() {
 var b1 = [
            'You are an only child.', 
            'You are an only child.', 
            'You are an only child.', 
            'You are an only child.', 
            'You are an only child.', 
            'You are an only child.', 
            'You have 1 sibling.',
            'You have 1 sibling.',
            'You have 1 sibling.',
            'You have 1 sibling.',
            'You have 1 sibling.', 
            'You have 2 siblings.',
            'You have 2 siblings.',
            'You have 2 siblings.',
            'You have 2 siblings.',
            'You have 3 siblings.',
            'You have 3 siblings.',
            'You have 4 siblings.',
            'You have 4 siblings.',
            'You have 5 siblings.',
          ];
    var dData = '';
    var dRoll = rolldice(0, (b1.length - 1));

    switch (true) {
        case (dRoll <= 5):
            // You are an only child
            dData += b1[dRoll] + '<br /><br />';
        break;

        case (dRoll >= 6 && dRoll <= 10):
            // You have 1 sibling
            dData += b1[dRoll];
            dData += '<ul><li>' + siblingIndividuality() + '<ul><li>[Viewpoint] ' + siblingViewpoint() + '</li></ul></li></ul>';
        break;

        case (dRoll >= 11 && dRoll <= 14):
            // You have 2 siblings
            dData += b1[dRoll];
            dData += '<ul>';
                
            for (i = 0; i < 2; i++) {
                dData += '<li>' + siblingIndividuality() + '<ul><li>[Viewpoint] ' + siblingViewpoint() + '</li></ul></li>';
            }

            dData += '</ul>';
        break;

        case (dRoll >= 15 && dRoll <= 16):
            // You have 3 siblings
            dData += b1[dRoll];
            dData += '<ul>';
                
            for (i = 0; i < 3; i++) {
                dData += '<li>' + siblingIndividuality() + '<ul><li>[Viewpoint] ' + siblingViewpoint() + '</li></ul></li>';
            }

            dData += '</ul>';
        break;

        case (dRoll >= 17 && dRoll <= 18):
            // You have 4 siblings
            dData += b1[dRoll];
            dData += '<ul>';
                
            for (i = 0; i < 4; i++) {
                dData += '<li>' + siblingIndividuality() + '<ul><li>[Viewpoint] ' + siblingViewpoint() + '</li></ul></li>';
            }

            dData += '</ul>';
        break;

        case (dRoll >= 19):
            // You have 5 siblings
            dData += b1[dRoll];
            dData += '<ul>';
                
            for (i = 0; i < 5; i++) {
                dData += '<li>' + siblingIndividuality() + '<ul><li>[Viewpoint] ' + siblingViewpoint() + '</li></ul></li>';
            }

            dData += '</ul>';
        break;
    }

    return dData;
}

function siblingIndividuality() {
 var b2 = [
            'Baby Sister.',
            'Slightly younger sister.',
            'Twin sister.',
            'Slightly older sister.',
            'Matriarch sister.',
            'Baby brother.',
            'Slightly younger brother.',
            'Twin brother.',
            'Slightly older brother.',
            'Patriarch brother.'
          ];

    var dRoll = rolldice(0, (b2.length - 1));

    return b2[dRoll];
}

function siblingViewpoint() {
 var b3 = [
            'Feelings are moot—your sibling is dead.',
            'Feelings are moot—your sibling is no longer around.',
            'The sibling is a sibling, love and rivalry will always be there.',
            'Your sibling is also your best friend.',
            'The sibling loves you but you don\’t see eye to eye.',
            'The sibling worships the very ground you walk on. You respect that.',
            'The sibling has issues with you, which may or may not be justified.',
            'The sibling and you don\’t talk. They may hate you; you may hate them.'
          ];

    var dRoll = rolldice(0, (b3.length - 1));
    var dData = '';
    
    switch(true) {
        case (dRoll == 0):
            dData += b3[dRoll];
            dData += '<ul><li>[Casualty] ' + casualty() + '</li></ul>';
        break;

        case (dRoll == 1):
            dData += b3[dRoll];
            dData += '<ul><li>[Separation] ' + separation() + '</li></ul>';
        break

        case (dRoll >= 2):
            dData += b3[dRoll];
        break;
    }

    return dData;
}

function lifeEpisodes(isApex) {
 var c1 = [
            '<b>Tragedy.</b> Something bad happened in your life.',
            '<b>Friendship.</b> You found a friend. Good for you. Gender and race are up to you. Friends are different than earned favors or informants.',
            '<b>Enemy.</b> Decide on who the person is, what caused it, and what the other will do when encountered. Gender and age are up to you.',
            '<b>Romance.</b> Aww…Sweet. You found someone important in your life.',
            '<b>Windfall.</b> Something good happened in your life.'
          ];

    var dRoll = rolldice(0, (c1.length - 1));
    var dData = '';

    switch(dRoll) {
        case 0:
            dData += c1[dRoll] + tragedy(isApex);
        break;

        case 1:
            dData += c1[dRoll] + friendship();
        break;

        case 2:
            dData += c1[dRoll] + '<ul>' + enemy() + enemyCause() + enemyWho() + enemyWhat() + enemyThrown() + '</ul>';
        break;

        case 3:
            dData += c1[dRoll] + romance();
        break;

        case 4:
            dData += c1[dRoll] + windfall(isApex);
        break;

        default:
            dData += c1[dRoll];
        break;
    }

    return dData;
}

function tragedy(isApex) {
 var c2 = [
            ['[Injury] You suffer a crippling wound.', 
                [ 
                    'Most of the damage is internal or psychological; most people don\’t notice.',
                    'You have scars or burns across your body, but most can be covered by clothes. If a critical hit is scored on you, you are stunned until the end of your next turn.',
                    'You suffered facial scars or burns. You have disadvantage with Charisma (Persuasion) checks.',
                    'You developed hearing problems. You have disadvantage with any ability check that requires hearing. If you also have the Bad Hearing shortcoming, you are completely deaf instead.',
                    'You developed a limp. It\’s noticeable and may require a cane. Your speed is reduced by 5 feet.',
                    'You lost a hand. Unless cybernetics have advanced far enough, your functionality is severely reduced. You lose the function of one hand.',
                    'An internal injury never fully healed. It\’s not visible, but it affects you. Your hit points are reduced by 2 at 1st level, and you gain 1 hit point less every additional level gained.',
                    'You lost an eye, replaced with a false eye or patch. Advances in cybernetics may mitigate this penalty—otherwise, you cannot score a critical hit.'
                ] 
            ],
            ['[Addiction] You developed a substance addiction. You can try to kick the habit in-game (you may kick it later in life habits), but it shouldn\’t be easy. If separated from your fix for more than a day, you are poisoned until your addiction is satisfied.' + (isApex ? ' You also can\'t use any apex talents.' : ''),
                [ 
                    'Caffeine', 'Caffeine', 'Caffeine', 'Caffeine',
                    'Chocolate', 'Chocolate', 'Chocolate', 'Chocolate',
                    'Alcohol', 'Alcohol', 'Alcohol',
                    'Cannabis', 'Cannabis', 'Cannabis',
                    'Tobacco', 'Tobacco',
                    '' + addictionDrugs() + '', '' + addictionDrugs() + '',
                    'Hallucinogens',
                    'Amphetamines',
                    'Opiods'
                ]
            ],
            ['[Psychological Trauma] You suffered an ordeal which left permanent emotional scars or even a behavioral addiction.',
                [ 
                    'You wake up every morning suddenly. You are slightly moody. You sweat on occasion in stressful situations. These are minor manifestations that don’t affect you greatly, but friends notice.',
                    'You wake up every morning suddenly. You are slightly moody. You sweat on occasion in stressful situations. These are minor manifestations that don’t affect you greatly, but friends notice.',
                    'You wake up every morning suddenly. You are slightly moody. You sweat on occasion in stressful situations. These are minor manifestations that don’t affect you greatly, but friends notice.',
                    'You wake up every morning suddenly. You are slightly moody. You sweat on occasion in stressful situations. These are minor manifestations that don’t affect you greatly, but friends notice.',
                    'You wake up every morning suddenly. You are slightly moody. You sweat on occasion in stressful situations. These are minor manifestations that don’t affect you greatly, but friends notice.',
                    'You\’re an alcoholic. If separated from alcohol for more than a day, you are poisoned until your addiction is satisfied.' + (isApex ? ' You also can\'t use any apex talents.' : ''),
                    'You developed a stutter, and have issues with public speaking. You have disadvantage with both Charisma (Persuasion) and Charisma (Intimidation) checks.',
                    'You suffer from nightmares. Even if no one notices, it affects you. After you wake from unconscious, you have disadvantage to ability checks and attack rolls for five minutes.'  + (isApex ? ' While suffering a nightmare, there is a 50% chance your apex talents manifest.' : ''),
                    'You suffer from migraines. You have disadvantage with Intelligence ability checks.',
                    'You love gambling, but this is not necessarily limited to games; you may place yourself at risk in order to achieve the same stimulus.',
                    'You suffer from obsessive compulsive disorder (OCD). ' + ocdCompulsion() + ' You must perform your compulsion once per day. You have disadvantage on ability checks until your compulsion is sated',
                    'You suffer from halucinations (tactial, auditory and/or visual). You have disadvantage on Wisdom (Perception) checks.',
                    'You suffer from flashbacks from a trauma (family violence, accident, combat, etc). You have disadvantage on Charisma (Persuasion) checks. You have advantage on Charisma (Intimidation) checks.',
                    'You suffer from paranoia (aliens, conspiracies, etc). You have disadvantage on Wisdom (Insight) checks.',
                ]
            ],
            ['[Loss] Lover, friend, or relative killed <ul><li>[Casualty] ' + casualty() + '</li></ul>',
                [ 'none' ]
            ],
            ['[Pursued by Criminals] You have crossed some very dangerous people and are now being hunted.',

                [ 
                    'You crossed a small gang, forcing you to avoid certain areas.',
                    'You crossed a small gang, forcing you to avoid certain areas.',
                    'You crossed a small gang, forcing you to avoid certain areas.',
                    'You crossed a small gang, forcing you to avoid certain areas.',
                    'You crossed a small gang, forcing you to avoid certain areas.',
                    'You crossed a small gang, forcing you to avoid certain areas.',
                    'A small crime organization put a mark on you.',
                    'A small crime organization put a mark on you.',
                    'A small crime organization put a mark on you.',
                    'A small crime organization put a mark on you.',
                    'A small crime organization put a mark on you.',
                    'You crossed a prominent crime family.',
                    'You crossed a prominent crime family.',
                    'You crossed a prominent crime family.',
                    'You crossed a prominent crime family.',
                    'You ticked off a major crime syndicate with connections across the land.',
                    'You ticked off a major crime syndicate with connections across the land.',
                    'You ticked off a major crime syndicate with connections across the land.',
                    'Turns out, you cut the finger of a massive criminal body with shell corporations and influence over governments.',
                    'Turns out, you cut the finger of a massive criminal body with shell corporations and influence over governments.'
                ]
            ],
            ['[Illness] You either contract a major illness or a hereditary disease rears its ugly head. You spend a time suffering from it.',
                [ 
                    'Stage 0: You contract an infectious disease and for a while the prognosis looked grim. Thankfully, you pulled through with only minor aftereffects.',
                    'Stage 0: You contract an infectious disease and for a while the prognosis looked grim. Thankfully, you pulled through with only minor aftereffects.',
                    'Stage 0: You contract an infectious disease and for a while the prognosis looked grim. Thankfully, you pulled through with only minor aftereffects.',
                    'Stage 0: You contract an infectious disease and for a while the prognosis looked grim. Thankfully, you pulled through with only minor aftereffects.',
                    'Stage 0: You contract an infectious disease and for a while the prognosis looked grim. Thankfully, you pulled through with only minor aftereffects.',
                    'Stage 0: You contract an infectious disease and for a while the prognosis looked grim. Thankfully, you pulled through with only minor aftereffects.',
                    'Stage 0: You contract an infectious disease and for a while the prognosis looked grim. Thankfully, you pulled through with only minor aftereffects.',
                    'Stage 0: You contract an infectious disease and for a while the prognosis looked grim. Thankfully, you pulled through with only minor aftereffects.',
                    'Stage 0: You contract an infectious disease and for a while the prognosis looked grim. Thankfully, you pulled through with only minor aftereffects.',
                    'Stage 0: You contract an infectious disease and for a while the prognosis looked grim. Thankfully, you pulled through with only minor aftereffects.',
                    'Stage 1: You cannot fully recover from your condition and must manage it with medication. If properly dosed, no one notices your situation. If you are denied your pill, injection, or treatment, you do not recover any Hit Dice after a long rest' + (isApex ? ' and cannot use any apex talents' : '') + '.',
                    'Stage 1: You cannot fully recover from your condition and must manage it with medication. If properly dosed, no one notices your situation. If you are denied your pill, injection, or treatment, you do not recover any Hit Dice after a long rest' + (isApex ? ' and cannot use any apex talents' : '') + '.',
                    'Stage 1: You cannot fully recover from your condition and must manage it with medication. If properly dosed, no one notices your situation. If you are denied your pill, injection, or treatment, you do not recover any Hit Dice after a long rest' + (isApex ? ' and cannot use any apex talents' : '') + '.',
                    'Stage 1: You cannot fully recover from your condition and must manage it with medication. If properly dosed, no one notices your situation. If you are denied your pill, injection, or treatment, you do not recover any Hit Dice after a long rest' + (isApex ? ' and cannot use any apex talents' : '') + '.',
                    'Stage 2: Despite regular medication, everyone that knows you is aware you\’ll never be 100%. You have disadvantage with Constitution ability checks. If you are denied your pill, injection, or treatment, you do not recover any Hit Dice after a long rest' + (isApex ? ' and cannot use any apex talents' : '') + '.',
                    'Stage 2: Despite regular medication, everyone that knows you is aware you\’ll never be 100%. You have disadvantage with Constitution ability checks. If you are denied your pill, injection, or treatment, you do not recover any Hit Dice after a long rest' + (isApex ? ' and cannot use any apex talents' : '') + '.',
                    'Stage 2: Despite regular medication, everyone that knows you is aware you\’ll never be 100%. You have disadvantage with Constitution ability checks. If you are denied your pill, injection, or treatment, you do not recover any Hit Dice after a long rest' + (isApex ? ' and cannot use any apex talents' : '') + '.',
                    'Stage 3: Your condition is apparent to most everyone. Friends worry; strangers often keep their distance. At the start of every morning, you suffer hit point loss equal to 10% of your total hit points. This can be healed through any available means. You have disadvantage with Constitution ability checks. If you are denied your pill, injection, or treatment, you do not recover any Hit Dice after a long rest' + (isApex ? ' and cannot use any apex talents' : '') + '.',
                    'Stage 3: Your condition is apparent to most everyone. Friends worry; strangers often keep their distance. At the start of every morning, you suffer hit point loss equal to 10% of your total hit points. This can be healed through any available means. You have disadvantage with Constitution ability checks. If you are denied your pill, injection, or treatment, you do not recover any Hit Dice after a long rest' + (isApex ? ' and cannot use any apex talents' : '') + '.',
                    'Stage 4: It\’s honestly a miracle you\’re still alive. There\’s no doubt that your lifespan has been reduced from an affliction that you suffer from daily. Your hit points are reduced by 2 at 1st level, and you gain 1 hit point less every additional level gained. At the start of every morning, you suffer hit point loss equal to 10% of your total hit points. This can be healed through any available means. You have disadvantage with Constitution ability checks. If you are denied your pill, injection, or treatment, you do not recover any Hit Dice after a long rest' + (isApex ? ' and cannot use any apex talents' : '') + '.'
                ]
            ],
            ['[Pursued by the Law] From tax evasion to premeditated murder, an arrest was issued with your face and name. You and/or the GM can decide if the accusation was legitimate or not. Perhaps you were framed. That aspect is up to choice (and should be assumed for the major crimes). The severity of the crime and the lengths people will go to your capture is not.',
                [ 
                    'You honestly don\’t know the big deal, but obviously someone does. Outside of a few police officer that know you, most others won\’t even bother chasing you.',
                    'You honestly don\’t know the big deal, but obviously someone does. Outside of a few police officer that know you, most others won\’t even bother chasing you.',
                    'You honestly don\’t know the big deal, but obviously someone does. Outside of a few police officer that know you, most others won\’t even bother chasing you.',
                    'You honestly don\’t know the big deal, but obviously someone does. Outside of a few police officer that know you, most others won\’t even bother chasing you.',
                    'You honestly don\’t know the big deal, but obviously someone does. Outside of a few police officer that know you, most others won\’t even bother chasing you.',
                    'You honestly don\’t know the big deal, but obviously someone does. Outside of a few police officer that know you, most others won\’t even bother chasing you.',
                    'It\’s a relatively minor offense (petty theft, drug use) in a small town, though still warranting jail time.',
                    'It\’s a relatively minor offense (petty theft, drug use) in a small town, though still warranting jail time.',
                    'It\’s a relatively minor offense (petty theft, drug use) in a small town, though still warranting jail time.',
                    'It\’s a relatively minor offense (petty theft, drug use) in a small town, though still warranting jail time.',
                    'It\’s a relatively minor offense (petty theft, drug use) in a small town, though still warranting jail time.',
                    'It\’s a major crime (grand theft, drug dealing), though you are relatively safe if you avoid the big cities.',
                    'It\’s a major crime (grand theft, drug dealing), though you are relatively safe if you avoid the big cities.',
                    'It\’s a major crime (grand theft, drug dealing), though you are relatively safe if you avoid the big cities.',
                    'It\’s a major crime (grand theft, drug dealing), though you are relatively safe if you avoid the big cities.',
                    'The state or local militia have posted rewards for information leading to your capture. This sort of crime (individual murder, organized crime, serial robbery, sex crimes) is considered severe.',
                    'The state or local militia have posted rewards for information leading to your capture. This sort of crime (individual murder, organized crime, serial robbery, sex crimes) is considered severe.',
                    'The state or local militia have posted rewards for information leading to your capture. This sort of crime (individual murder, organized crime, serial robbery, sex crimes) is considered severe.',
                    'A national police force is dedicated to your capture. Information regarding you has spread to every corner of the globe. This crime is nothing less than terrorism, spree killings, or serial murder.',
                    'A national police force is dedicated to your capture. Information regarding you has spread to every corner of the globe. This crime is nothing less than terrorism, spree killings, or serial murder.'
                ]
            ],
            ['[Debt] What you owe can be financial or personal. It could be to a government or to one person.',
                [ 
                   'Someone, somewhere, did you favor, something you needed at the time. This is not entirely financial, but they can call on you anytime for help.',
                   'Someone, somewhere, did you favor, something you needed at the time. This is not entirely financial, but they can call on you anytime for help.', 
                   'Someone, somewhere, did you favor, something you needed at the time. This is not entirely financial, but they can call on you anytime for help.', 
                   'Someone, somewhere, did you favor, something you needed at the time. This is not entirely financial, but they can call on you anytime for help.', 
                   'Someone, somewhere, did you favor, something you needed at the time. This is not entirely financial, but they can call on you anytime for help.', 
                   'Someone, somewhere, did you favor, something you needed at the time. This is not entirely financial, but they can call on you anytime for help.', 
                   'You were saddled with incredible amounts of debt, which thankfully you have resolved in your later life. However, the stigma of that liability lingers, preventing you from taking chances financially or even getting approval for credit.',
                   'You were saddled with incredible amounts of debt, which thankfully you have resolved in your later life. However, the stigma of that liability lingers, preventing you from taking chances financially or even getting approval for credit.',
                   'You were saddled with incredible amounts of debt, which thankfully you have resolved in your later life. However, the stigma of that liability lingers, preventing you from taking chances financially or even getting approval for credit.',
                   'You were saddled with incredible amounts of debt, which thankfully you have resolved in your later life. However, the stigma of that liability lingers, preventing you from taking chances financially or even getting approval for credit.',
                   'You were saddled with incredible amounts of debt, which thankfully you have resolved in your later life. However, the stigma of that liability lingers, preventing you from taking chances financially or even getting approval for credit.',
                   'Your debt derives from some very bad decisions, decisions that you are still paying for. Your debt is $' + numFormat((rolldice(1, 6) * 100)) + '. When paid by a later event or in game, your debt is fulfilled.',
                   'Your debt derives from some very bad decisions, decisions that you are still paying for. Your debt is $' + numFormat((rolldice(1, 6) * 100)) + '. When paid by a later event or in game, your debt is fulfilled.',
                   'Your debt derives from some very bad decisions, decisions that you are still paying for. Your debt is $' + numFormat((rolldice(1, 6) * 100)) + '. When paid by a later event or in game, your debt is fulfilled.',
                   'Your debt derives from some very bad decisions, decisions that you are still paying for. Your debt is $' + numFormat((rolldice(1, 6) * 100)) + '. When paid by a later event or in game, your debt is fulfilled.',
                   'There is not legal recourse; this is bad. You owe some powerful people a lot of money. You better appease them or make installments; otherwise you might find a price on your head. Your debt is $' + numFormat((rolldice(1, 6) * 1000)) + '. When paid by a later event or in game, your debt is fulfilled.',
                   'There is not legal recourse; this is bad. You owe some powerful people a lot of money. You better appease them or make installments; otherwise you might find a price on your head. Your debt is $' + numFormat((rolldice(1, 6) * 1000)) + '. When paid by a later event or in game, your debt is fulfilled.',
                   'There is not legal recourse; this is bad. You owe some powerful people a lot of money. You better appease them or make installments; otherwise you might find a price on your head. Your debt is $' + numFormat((rolldice(1, 6) * 1000)) + '. When paid by a later event or in game, your debt is fulfilled.',
                   'In cash or blood, you must repay this obligation. In lieu of a very dangerous mission, your debt is massive. Your debt is $' + numFormat((rolldice(1, 6) * 10000)) + '. When paid by a later event or in game, your debt is fulfilled.',
                   'In cash or blood, you must repay this obligation. In lieu of a very dangerous mission, your debt is massive. Your debt is $' + numFormat((rolldice(1, 6) * 10000)) + '. When paid by a later event or in game, your debt is fulfilled.'
                ]
            ],
            ['[Imprisonment] You’ve been either kidnapped or sent to prison. Whether or not it\’s warranted or how you get out at the end is up to you or the GM.' + (isApex ? '<br/>It is also very likely your apex talents were discovered and an organization wishing to control you managed to finally catch up. If apex related, you never get out, and must roll a later life event as an appropriate windfall, or even by the tragedies "pursued by the law" or "pursued by criminals or hidden society." If so, you can either be released under monitoring, or most likely escape, resulting in a hunt. There is also the possibility this imprisonment was imposed because of your apex potential, and it was here where your talents emerged. Either that, or something occurred there that made your more powerful. There is a 50% chance you gain 1 apex talent, though only one can be achieved this way.' : ''),
                [ 'You spent ' + rolldice(1, 20) + ' month(s) imprisoned' + (isApex ? ' and if apex related, you have potential to gain ' + (rolldice(1, 2) - 1) + ' apex talents' : '') + '.']
            ],
            ['[Failure] Your career has faltered. Something you have been working on for a very long time has failed miserably. You may need to reconsider your goals, perhaps even your direction in life.',
                [ 
                    'The failure cost you financially. You lose $' + numFormat((rolldice(3, 18) * 10)) + '  from starting money.',
                    'The failure cost you financially. You lose $' + numFormat((rolldice(3, 18) * 10)) + ' from starting money.',
                    'The failure cost you financially. You lose $' + numFormat((rolldice(3, 18) * 10)) + ' from starting money.',
                    'The failure cost you financially. You lose $' + numFormat((rolldice(3, 18) * 10)) + ' from starting money.',
                    'The failure cost you financially. You lose $' + numFormat((rolldice(3, 18) * 10)) + ' from starting money.',
                    'The failure cost you financially. You lose $' + numFormat((rolldice(3, 18) * 10)) + ' from starting money.',
                    'The failure cost you financially. You lose $' + numFormat((rolldice(3, 18) * 10)) + ' from starting money.',
                    'You lose your current status at your employment. If you had a rank, you are demoted. If it was a corporate job, you were banished to a lower floor.',
                    'You lose your current status at your employment. If you had a rank, you are demoted. If it was a corporate job, you were banished to a lower floor.',
                    'You lose your current status at your employment. If you had a rank, you are demoted. If it was a corporate job, you were banished to a lower floor.',
                    'You lose your current status at your employment. If you had a rank, you are demoted. If it was a corporate job, you were banished to a lower floor.',
                    'You lose your current status at your employment. If you had a rank, you are demoted. If it was a corporate job, you were banished to a lower floor.',
                    'You were fired outright or placed on leave. If in the military, you are busted down to private.',
                    'You were fired outright or placed on leave. If in the military, you are busted down to private.',
                    'You were fired outright or placed on leave. If in the military, you are busted down to private.',
                    'You were fired outright or placed on leave. If in the military, you are busted down to private.',
                    'You were fired outright or placed on leave. If in the military, you are busted down to private.',
                    'You lose everything, your position, your rank, and any hope of following that career again. What did you do? It might have been unethical. Was it warranted, or were you framed?',
                    'You lose everything, your position, your rank, and any hope of following that career again. What did you do? It might have been unethical. Was it warranted, or were you framed?'
                ]
            ]
          ];

    var dRoll = rolldice(0, (c2.length - 1));

    //debug
    //var dRoll = 8;
    // var dBug = 'dRoll=' + dRoll + ' return=' + c2[dRoll][1];
    // alert(dBug);

    dData = '';

    if(c2[dRoll][1][0] == 'none') {
        dData += '<ul><li>' + c2[dRoll][0] + '</li></ul>';
    } else {
        dData += '<ul><li>' + c2[dRoll][0];
        var dRollx = rolldice(0, (c2[dRoll][1].length - 1));
        dData += '<ul><li>' + c2[dRoll][1][dRollx] + '</li></ul></li></ul>';
    }

    return dData;
}

function ocdCompulsion() {
 var c2ax = [
            '[Compulsion] Washing and Cleaning (self, environment, clothes, etc).',
            '[Compulsion] Checking (self harm, doors locked, things done correctly, didn\'t harm others, etc).',
            '[Compulsion] Repeating (body movements, routine activities, etc).',
            '[Compulsion] Rereading or Rewriting (multiples, specific order, etc).',
            '[Compulsion] Canceling (replacing bad words, 12 cookies-- but drinks diet soda, etc).'
          ];

    var dRoll = rolldice(0, (c2ax.length - 1));

    return c2ax[dRoll];
}

function addictionDrugs() {
 var c2a = [
            'Anabolic Steroids.',
            'Stimulants.',
            'Depressants.',
            'Painkillers.'
          ];

    var dRoll = rolldice(0, (c2a.length - 1));

    return c2a[dRoll];
}

function windfall(isApex) {
 var c3 = [
            ['[Earned Favor] Someone appreciates your actions. You might have saved a life or offered critical advice at the right time. A debt is owed that you can call on. How you can call on this favor and how often you can be determined below. A favor can supply equipment, transportation, access, money, or even military support.', 
                [ 
                    'threetables', 
                        [
                            'A relative nobody but who obviously has connections you don\’t know about.',
                            'A relative nobody but who obviously has connections you don\’t know about.',
                            'A relative nobody but who obviously has connections you don\’t know about.',
                            'A relative nobody but who obviously has connections you don\’t know about.',
                            'A relative nobody but who obviously has connections you don\’t know about.',
                            'The military or police commander.',
                            'The military or police commander.',
                            'The military or police commander.',
                            'The military or police commander.',
                            'A lord, small town mayor, or the president of small company.',
                            'A lord, small town mayor, or the president of small company.',
                            'A lord, small town mayor, or the president of small company.',
                            'The patriarch or matriarch of a major crime family.',
                            'The patriarch or matriarch of a major crime family.',
                            'The patriarch or matriarch of a major crime family.',
                            'The president of a corporation. In medieval times, a duke or baron.',
                            'The president of a corporation. In medieval times, a duke or baron.',
                            'Royalty or the president of a multinational corporation.',
                            'Royalty or the president of a multinational corporation.',
                            'This person runs a country.'
                        ],
                        [
                            'The debtor is limited to what she can accomplish by herself.',
                            'The debtor is limited to what she can accomplish by herself.',
                            'The debtor is limited to what she can accomplish by herself.',
                            'The debtor is limited to what she can accomplish by herself.',
                            'The debtor is limited to what she can accomplish by herself.',
                            'The debtor is limited to what she can accomplish by herself.',
                            'The debtor is limited to what she can accomplish by herself.',
                            'You can call on them for a single favor a level, or one big favor that will resolve the obligation.',
                            'You can call on them for a single favor a level, or one big favor that will resolve the obligation.',
                            'You can call on them for a single favor a level, or one big favor that will resolve the obligation.',
                            'You can call on them for a single favor a level, or one big favor that will resolve the obligation.',
                            'You can call on them for a single favor a level, or one big favor that will resolve the obligation.',
                            'You can call on them for a single favor a level, or one big favor that will resolve the obligation.',
                            'You can call on them, big or small, but you are limited to six favors total.',
                            'You can call on them, big or small, but you are limited to six favors total.',
                            'You can call on them, big or small, but you are limited to six favors total.',
                            'You can call on them, big or small, but you are limited to six favors total.',
                            'You can call on them, big or small, but you are limited to six favors total.',
                            'You can call on them, big or small, but are limited to two favors per level.',
                            'You can call on them, big or small, but are limited to two favors per level.'
                        ],
                        [
                            'The debt is owed by a single person who can or will only supply oneself.',
                            'The debt is owed by a single person who can or will only supply oneself.',
                            'The debt is owed by a single person who can or will only supply oneself.',
                            'The debt is owed by a single person who can or will only supply oneself.',
                            'The debt is owed by a single person who can or will only supply oneself.',
                            'The debt is owed by a single person who can or will only supply oneself.',
                            'The debtor can bring in a small group, like a gang, retinue, or a few employees.',
                            'The debtor can bring in a small group, like a gang, retinue, or a few employees.',
                            'The debtor can bring in a small group, like a gang, retinue, or a few employees.',
                            'The debtor can bring in a small group, like a gang, retinue, or a few employees.',
                            'The debtor can bring in a small group, like a gang, retinue, or a few employees.',
                            'The debtor will bring in dozens of people if necessary, calling on the right people for the right job.',
                            'The debtor will bring in dozens of people if necessary, calling on the right people for the right job.',
                            'The debtor will bring in dozens of people if necessary, calling on the right people for the right job.',
                            'The debtor will bring in dozens of people if necessary, calling on the right people for the right job.',
                            'The debtor has power and influence across hundreds, and can call on favors as well.',
                            'The debtor has power and influence across hundreds, and can call on favors as well.',
                            'The debtor has power and influence across hundreds, and can call on favors as well.',
                            'The debtor will move heaven and earth to appease you and may be able to do so. You want an army?',
                            'The debtor will move heaven and earth to appease you and may be able to do so. You want an army?'
                        ]
                ] 
            ],
            ['[Informant] Differentiated from favor, this is a connection that supplies information or their skill when called upon. This is probably someone you helped or a friend in a position of access. An informant has one dominant skill, rolled with a +8 bonus—this check has advantage. You can call on an informant once a week. The informant will never put oneself at risk and won’t have access to anything outside of what’s around.',
                [ 
                    'Professor. Intelligence (History)',
                    'Scientist. Intelligence (Nature / Sciences)',
                    'Doctor. Wisdom (Medicine)',
                    'Hacker. Intelligence (Computer Use)',
                    'Engineer. Intelligence (Engineering)',
                    'Priest. Intelligence (Religion)',
                    'Entertainer. Charisma (Performance)',
                    'Charlatan. Charisma (Deception)',
                    'Private Investigator. Intelligence (Investigation)',
                    'Survivalist. Wisdom (Survival)'
                ]
            ],
            ['[Wealth] What a stroke of luck, you\’ve come into some money. Don\’t spend it all at once.',
                [ 
                    'It wasn\’t much, a tax refund probably. You gain $' + numFormat((rolldice(3, 18) * 10)) + '.',
                    'It wasn\’t much, a tax refund probably. You gain $' + numFormat((rolldice(3, 18) * 10)) + '.',
                    'It wasn\’t much, a tax refund probably. You gain $' + numFormat((rolldice(3, 18) * 10)) + '.',
                    'It wasn\’t much, a tax refund probably. You gain $' + numFormat((rolldice(3, 18) * 10)) + '.',
                    'It wasn\’t much, a tax refund probably. You gain $' + numFormat((rolldice(3, 18) * 10)) + '.',
                    'It wasn\’t much, a tax refund probably. You gain $' + numFormat((rolldice(3, 18) * 10)) + '.',
                    'It wasn\’t much, a tax refund probably. You gain $' + numFormat((rolldice(3, 18) * 10)) + '.',
                    'You received a bonus, a commission, or a bank error in your favor. You gain $' + numFormat((rolldice(6, 36) * 10)) + '.',
                    'You received a bonus, a commission, or a bank error in your favor. You gain $' + numFormat((rolldice(6, 36) * 10)) + '.',
                    'You received a bonus, a commission, or a bank error in your favor. You gain $' + numFormat((rolldice(6, 36) * 10)) + '.',
                    'You received a bonus, a commission, or a bank error in your favor. You gain $' + numFormat((rolldice(6, 36) * 10)) + '.',
                    'You received a bonus, a commission, or a bank error in your favor. You gain $' + numFormat((rolldice(6, 36) * 10)) + '.',
                    'You received a bonus, a commission, or a bank error in your favor. You gain $' + numFormat((rolldice(6, 36) * 10)) + '.',
                    'You’ve had a good night gambling, or finished a long-term project. Maybe you won a contest. You gain $' + numFormat((rolldice(1, 4) * 1000)) + '.',
                    'You’ve had a good night gambling, or finished a long-term project. Maybe you won a contest. You gain $' + numFormat((rolldice(1, 4) * 1000)) + '.',
                    'You’ve had a good night gambling, or finished a long-term project. Maybe you won a contest. You gain $' + numFormat((rolldice(1, 4) * 1000)) + '.',
                    'You’ve had a good night gambling, or finished a long-term project. Maybe you won a contest. You gain $' + numFormat((rolldice(1, 4) * 1000)) + '.',
                    'You’ve had a good night gambling, or finished a long-term project. Maybe you won a contest. You gain $' + numFormat((rolldice(1, 4) * 1000)) + '.',
                    'This is nothing short of a lottery win, inheritance, or a bank heist. However, the money is put aside for a rainy day. You gain the following bonuses when achieving the listed level: 1st level - $500; 5th level – 2,500; 10th level - $10,000; 15th level – $55,000.',
                    'This is nothing short of a lottery win, inheritance, or a bank heist. However, the money is put aside for a rainy day. You gain the following bonuses when achieving the listed level: 1st level - $500; 5th level – 2,500; 10th level - $10,000; 15th level – $55,000.'
                ]
            ],
            ['[' + (isApex ? 'Apex / ' : '') + 'Combat Training] You gain admittance in a self-defense Class or find a martial-arts / weapons teacher' + (isApex ? ' or stumble across someone willing to train your apex talents' : '') + '. You spend an extended time specializing in a craft apart from your usual training. Each time you gain this windfall, you learn an additional tier.' + (isApex ? ' Select Combat or Apex tiers.' : ''),
                [ 
                    'Combat Tier 1: You gain ' + rolldice(1, 4) + ' weapon proficiencies.<br />Combat Tier 2: You gain a +2 bonus to initiative.<br/>Combat Tier 3: Your speed increases by +5 feet.<br />Combat Tier 4: You gain 1 feat.' + (isApex ? '<br />Apex Tier 1: When pushing apex, if you fail your check, you reduce your final role by 3 when calculating consequence.<br/>Apex Tier 2: You gain 1 apex talent.<br/>Apex Tier 3: When pushing apex, if you fail your check, you reduce your final role by 3 (6 total) when calculating consequence.<br/>Apex Tier 4: You gain 1 apex talent.' : ''),
                ]
            ],
            ['[Education Grant] People believe you\’re smart and throw money your way in order to develop your skills further. Each time you gain an education grant, you gain proficiency in one skill or tool of your choice as well as one additional language.',
                [ 'none' ]
            ],
            ['[Recognition] You have been bestowed a well-deserved award, perhaps a gilded trophy. Maybe a medal. This doesn\’t assume a contest. If in the military, you receive medals; you don\’t win them. If in academia, you receive acknowledgement for a peer-reviewed paper which has advanced your field. You have advantage on Charisma (Persuasion) checks with other people in in the same field that know of your achievements.',
                [ 'none' ]
            ],
            [(isApex ? '[Apex Emergence] One of two possibilities occur. Firstly, your talents manifested early, and what occurred was an unexpected surge in power, probably dramatic, perhaps coinciding with the revelation to others that you are special. Secondly, your talents hadn\'t emerged at all, and suddenly express themselves in a extraordinary fashion. This type of emergence is generally non-destructive, or if it is, has minor collateral effects. You gain 1 apex talent. Only 1 apex talent can be acquired this way.' : '[Positive Side Effect] Well, that was un-expected. You have been subjected to a medical experiment, a yet untested treatment to a condition you suffer from, or something latent hidden for many years has finally manifested itself. Roll on the Genetic Benefit Table'),
                [ 'none' ]
            ],
            ['[Reputation/Rank] If in the military, you achieve a promotion. If on contract, you are able to raise your prices based on reputation alone. You are given more authority, influence over underlings or employees. This may have reaching aftereffects in the game. You have advantage on Charisma (Intimidation) checks with other people under you com-mand or influence.',
                [ 'none' ]
            ],
            ['[Recovery] You recover from one effect from the Tragedy table you are suffering from (chosen by you or the GM).',
                [ 'none' ]
            ],
            ['[Personal Treasure] You discovered, was bequeathed, or were given something of value, something you treasure more than most other things, something you neither should sell or even want to (not that you would get anything, as selling it would only net you 1/10 its original value. Select one item worth $5,000 or less as your item.',
                [ 'none' ]
            ]
          ];

    var dRoll = rolldice(0, (c3.length - 1));

    dData = '';

    if(c3[dRoll][1][0] == 'none') {
        dData += '<ul><li>' + c3[dRoll][0] + '</li></ul>';
    } else {
        if(c3[dRoll][1][0] == 'threetables') {
            dData += '<ul><li>' + c3[dRoll][0];

            var dRollx = rolldice(0, (c3[dRoll][1][1].length - 1));
            dData += '<ul><li>[Identity] ' + c3[dRoll][1][1][dRollx];

            var dRollx = rolldice(0, (c3[dRoll][1][2].length - 1));
            dData += '<ul><li>[Frequency] ' + c3[dRoll][1][2][dRollx] + '</li>';

            var dRollx = rolldice(0, (c3[dRoll][1][3].length - 1));
            dData += '<li>[Influence] ' + c3[dRoll][1][3][dRollx] + '</li></ul></li></ul></li></ul>';

        } else {
            dData += '<ul><li>' + c3[dRoll][0];
            var dRollx = rolldice(0, (c3[dRoll][1].length - 1));
            dData += '<ul><li>' + c3[dRoll][1][dRollx] + '</li></ul></li></ul>';
        }
    }

    return dData;
}

function friendship() {
 var d1 = [
            'You reconnect with a relative (cousin, uncle, lost sibling, etc.)',
            'A previous romantic interest. Either your separated prior and reconnected later, or the relationship didn\’t work and you remained as friends.',
            'An old childhood friend, either that you\’ve never lost contact with or one you bumped into and realized no time had really passed.',
            'A co-worker, which could mean a tedious day job or a comrade you shared basic training with.',
            'You owed this person a favor, or they owed you. Turns out you two both like the same things. The debt has long since been paid.',
            'This person had known your family or mutual friends for years and you always considered him/her as a big brother / big sister. Alternatively, you\’ve known this person through his/her family or mutual friends for years and you always considered him/her as a kid brother / kid sister.',
            'It started as a teacher or mentor relationship, but after the classes were concluded, you two stayed in touch.',
            'An old enemy, if you have one, and it makes sense. You two came to an understanding.',
            'You two met through common interests or mutual friends. Consider it boring but it\’s also common.',
            'He or she was more like a foster-parent, or rather the closest one you had to one, or the one you wished you had.'
          ];

    var dRoll = rolldice(0, (d1.length - 1));
    var dData = '';

    dData += '<ul><li>' + d1[dRoll] + '</li></ul>';

    return dData;
}

function enemy() {
 var e1 = [
            'Alas, not all friendships end well. A friend you picked up becomes an enemy.',
            'A relationship you are currently in ends very badly. Or else someone you used to date comes back with an aim to destroy your life.',
            'Regardless of blood, some lines still cannot be crossed. A relative is no longer a friend.',
            'Either someone that bullied you or some-one you bullied in your youth returns.',
            'A coworker in a higher position wants to keep you down. As long as he/she is above you, you\’ll never advance.',
            'Someone under your authority wants to bring you down to his/her level.',
            'Someone you work with (a co-worker on equal footing) has it in for you.',
            'A criminal is out for you.',
            'Someone with a lot of weaponry (like someone in military or law enforce-ment) really doesn\’t like you.',
            'Make sure you filed your taxes, because even the slightest slip could bring down the wrath from this government official with a lot of bureaucratic clout.',
          ];

    var dRoll = rolldice(0, (e1.length - 1));
    var dData = '';

    dData += '<li>' + e1[dRoll] + '</li>';

    return dData;
}

function enemyCause() {
 var e2 = [
            [
                'Either you or the enemy caused the other to lose face (not literal) or position.',
                [ 'none' ]
            ],
            [
                'You caused your enemy a physical disability.',
                [
                    'Facial scars or burns.',
                    'Developed hearing problems',
                    'Developed a limp',
                    'Lost a hand',
                    'Lost an eye'
                ]
            ],
            [
                'You or your enemy caused the enemy to lose a loved one.',
                [ 'none' ]
            ],
            [
                'You or your enemy exposed a dark secret of the other that upset the other\’s life (but did not involve criminal proceed-ings).',
                [ 'none' ]
            ],
            [
                'You or your enemy was humiliated. Sometimes, that\’s enough.',
                [ 'none' ]
            ],
            [
                'There was a betrayal or abandonment.',
                [ 'none' ]
            ],
            [
                'You or your enemy was responsible for jail time.',
                [
                    'You went to jail for ' + rolldice(1, 20) + ' month(s).',
                    'Your enemy went to jail for ' + rolldice(1, 20) + ' month(s).'
                ]
            ],
            [
                'You or your enemy just hates the other\’s stupid, stupid face.',
                [ 'none' ]
            ],
            [
                'You or your enemy cost the other a job or a lucrative deal.',
                [ 'none' ]
            ],
            [
                'You or your enemy foiled the other\’s cunning plan.',
                [ 'none' ]
            ]
          ];

    var dRoll = rolldice(0, (e2.length - 1));
    var dData = '';

    if(e2[dRoll][1][0] == 'none') {
        dData += '<li>[Cause] ' + e2[dRoll][0] + '</li>';
    } else {
        dData += '<li>[Cause] ' + e2[dRoll][0];
        var dRollx = rolldice(0, (e2[dRoll][1].length - 1));
        dData += '<ul><li>' + e2[dRoll][1][dRollx] + '</li></ul></li>';
    }

    return dData;
}

function enemyWho() {
 var e3 = [
            'Your enemy is ticked off with you. You don\’t fully get it, and probably think it\’s being really overinflated. Someone needs a hug.',
            'Your enemy is your enemy. It doesn\’t matter that he or she doesn\’t hold a grudge; you do.',
            'It\’s totally mutual for both of you.'
          ];

    var dRoll = rolldice(0, (e3.length - 1));
    var dData = '';

    dData += '<li>[Who ticked who off] ' + e3[dRoll] + '</li>';

    return dData;
}

function enemyWhat() {
 var e4 = [
            'The crossed individual (or both) will try to kill the other when given the chance, no remorse. Is that going too far?',
            'The crossed individual (or both) wants to beat the living snot out of the other. Maybe it\’s something you both need to get out of your system.',
            'The crossed individual (or both) wants to destroy the other\’s life, to suffer for years and years.',
            'The crossed individual (or both) have been prepping some choice zingers to fling at the other at the first opportunity.',
            'It\’s just best you just avoid each other.'
          ];

    var dRoll = rolldice(0, (e4.length - 1));
    var dData = '';

    dData += '<li>[Who does what] ' + e4[dRoll] + '</li>';

    return dData;
}

function enemyThrown() {
 var e5 = [
            'Despite any authority, your enemy will only handle matters personally.',
            'Despite any authority, your enemy will only handle matters personally.',
            'Despite any authority, your enemy will only handle matters personally.',
            'Despite any authority, your enemy will only handle matters personally.',
            'Despite any authority, your enemy will only handle matters personally.',
            'Despite any authority, your enemy will only handle matters personally.',
            'Your enemy can bring in a small group, like a gang, retinue, or a few employees. A line is drawn about bringing in more.',
            'Your enemy can bring in a small group, like a gang, retinue, or a few employees. A line is drawn about bringing in more.',
            'Your enemy can bring in a small group, like a gang, retinue, or a few employees. A line is drawn about bringing in more.',
            'Your enemy can bring in a small group, like a gang, retinue, or a few employees. A line is drawn about bringing in more.',
            'Your enemy can bring in a small group, like a gang, retinue, or a few employees. A line is drawn about bringing in more.',
            'Your enemy will bring in dozens of people if necessary, calling on the right people for the right job.',
            'Your enemy will bring in dozens of people if necessary, calling on the right people for the right job.',
            'Your enemy will bring in dozens of people if necessary, calling on the right people for the right job.',
            'Your enemy will bring in dozens of people if necessary, calling on the right people for the right job.',
            'Your enemy has power and influence across hundreds, and can call on favors as well.',
            'Your enemy has power and influence across hundreds, and can call on favors as well.',
            'Your enemy has power and influence across hundreds, and can call on favors as well.',
            'Your enemy will move heaven and earth to appease you and may be able to do so. You want an army?',
            'Your enemy will move heaven and earth to appease you and may be able to do so. You want an army?'
          ];

    var dRoll = rolldice(0, (e5.length - 1));
    var dData = '';

    dData += '<li>[What can be thrown] ' + e5[dRoll] + '</li></ul>';

    return dData;
}

function romance() {
 var f1 = [
            'You met someone, dated for a spell, but ultimately it didn’t work out after only a few weeks or months. The break up might not have been mutual, but these things happen all the time.',
            'You met, are still together, but you can’t see it lasting. <ul><li>[Feelings] ' + romanceFeelings() + '</li></ul>',
            'You met and are still together. This may be the one.',
            'You met someone, but from the beginning, there were complications. <ul><li>[Issues] ' + romanceIssues() + '</li><li>[Feelings] ' + romanceFeelings() + '</li></ul>',
            'Tragic Love Why? WHY? <ul><li>[MisFortune] ' + romanceMisfortune() + '</li></ul>'
          ];

    var dRoll = rolldice(0, (f1.length - 1));
    var dData = '';

    dData += '<ul><li>' + f1[dRoll] + '</li></ul>';

    return dData;
}

function romanceIssues() {
 var f2 = [
            'Your family and/or friends hate your romantic interest.',
            'Your romantic interest\’s family and/or friends hate you.',
            'There is a romantic rival involved trying to divide you to. Who the rival is interested in can be chosen or randomized.',
            'You fight constantly.', 
            'You are professional rivals.',
            'There is a lot of jealously between you to.',
            'One of you two had an affair and the other found out.', 
            'The both of you come from different walks of life, and it puts pressure on the relationship. There may not be internal pressures, but there may be external ones.', 
            'The two of you differ in ethnicity or race. There may not be internal pressures, but there may be external ones.',
            'There are money problems; aren’t there always money problems?'
          ];

    var dRoll = rolldice(0, (f2.length - 1));
    var dData = '';

    dData += f2[dRoll];

    return dData;
}

function romanceMisfortune() {
 var f3 = [
            'Sometimes bad things happen, but the relationship survives it.',
            'You break up. It just was never going to work out—the separation is mutual.',
            'You dumped your romantic interest.', 
            'Your romantic interest dumped you.', 
            'You two are separated. <ul><li>[Separation] ' + separation() + '.</li></ul>',
            'Your romantic interest has died. <ul><li>[Casualty] ' + casualty() + '</li></ul>'
          ];

    var dRoll = rolldice(0, (f3.length - 1));
    var dData = '';

    dData += f3[dRoll];

    return dData;
}

function romanceFeelings() {
 var f4 = [
            'Despite everything (and there are a lot), you still love each other.',
            'Despite everything (and there are a lot), you still love each other.', 
            'Your romantic interest appears to have issues, but won\’t leave you. Why?',
            'You have issues, but you won\’t leave your romantic interest. Why?',
            'You both have issues—the relationship should have ended, but it doesn\’t. Something is holding you together.',
            'Your romantic interest still loves you; you\’re not so certain.',
            'You still love your romantic interest. You are worried it is no longer reciprocated.',
            'You\’re drifting apart from mutual apathy.',
            'You\’ll always be friends, but you fear the spark has faded.', 
            'Screw it. It\’s over.'
          ];

    var dRoll = rolldice(0, (f4.length - 1));
    var dData = '';

    dData += f4[dRoll];

    return dData;
}

// ////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Genetic benefit functions below ////////////////////////////////////////////////////////////////////////////
// ////////////////////////////////////////////////////////////////////////////////////////////////////////////

function geneticBenefit() {
 var gb1 = [
            '<b>Skill / Tool Proficiency.</b> You are adept at one thing since birth, a calling. You gain proficiency in one skill or tool of your choice.',
            '<b>Enhanced Secondary Senses.</b> A connoisseur, you have advantage with any Wisdom (Perception) checks regarding taste or smell.',
            '<b>Night Eyes.</b> You have superior vision in dark and dim conditions. You can see in dim light within 60 feet of you as if it were bright light, and in darkness as if it were dim light. You can\’t discern color in darkness, only shades of gray.',
            '<b>Disciplined Lungs.</b> You\’ve always had the capacity to hold your breath longer than others. You can go without oxygen for as many minutes as twice your Constitution modifier.',
            '<b>Extreme Fortitude.</b> You gain 2 additional hit points at 1st level, plus 1 additional hit point every additional level.',
            '<b>Light Sleeper.</b> It\’s been a positive and a negative, but you cannot be surprised by sleeping. Alas, it can also be difficult to get a proper night\’s sleep.',
            '<b>Short Sleeper.</b> You don\’t need much. You only require 3 hours of sleep per night to function, and a good night\’s sleep is only 4 hours.',
            '<b>Eidetic Memory.</b> You remember nearly everything. You automatically pass any Intelligence checks to recall any information you have been exposed to.',
            '<b>Empathy.</b> You\’ve always been able to understand someone\’s emotional state, allowing for sympathy or manipulation. You gain a +2 bonus to Wisdom (Insight).',
            '<b>Extra Fatigue.</b> You\’ve always been running. You can ignore level 1 and 2 exhaustion effects.',
            '<b>Fashion Sense.</b> You look good in anything, from haute couture to dollar store rejects. You have a +1 bonus to all Charisma ability checks.',
            '<b>Quick Healer.</b> Very useful when you were a child—you regain 1 additional spent Hit Die when you take a long rest.',
            '<b>High Pain Threshold.</b> You can take a punch. When reduced to zero hit points, you do not fall unconscious until you fail your first death save.',
            '<b>Disease Immunity.</b> You rarely get sick. You have advantage on saving throws against disease.',
            '<b>Poison Immunity.</b> Tastes minty. You have advantage on saving throws against poison.',
            '<b>Speed Boost.</b> Limber. You gain a +5 foot bonus to speed.',
            '<b>Strong Will.</b> Not easy to stare down. You have advantage with Wisdom saving throws; you also have proficiency with Wisdom (Intimidation).',
            '<b>Toughness.</b> Each time you suffer damage from a piercing or slashing weapon, you suffer 2 fewer points of damage.',
            '<b>Nimbleness.</b> You can move through the space of any creature that is of a size larger than yours.',
            '<b>Ornery.</b> When you score a critical hit with a melee weapon attack, you can roll one of the weapon\’s damage dice one additional time and add it to the extra damage of the critical hit.'
          ];

    var dRoll = rolldice(0, (gb1.length - 1));
    var dData = '';

    dData += gb1[dRoll];

    return dData;
}

// ////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Shortcomings functions below ///////////////////////////////////////////////////////////////////////////////
// ////////////////////////////////////////////////////////////////////////////////////////////////////////////

function shortComings() {
 var sc1 = [
            '<b>Bad Eyes.</b> It happens to everyone. You need glasses. Without them, you have disadvantage with Wisdom (Perception) checks when using your eyes.',
            '<b>Long Sleeper.</b> You get…headaches. You need to have at least 8 hours of sleep a night to qualify for having a long rest.',
            '<b>Bad Hearing.</b> I said, you need hearing aids. Without them, you have disadvantage with Wisdom (Perception) checks with them.',
            '<b>Hairless.</b> You have no hair. Anywhere. You have disadvantage with Charisma (Persuasion) checks.',
            '<b>Dwarfism.</b> The accepted term is \"little person\"—and while rumors of short people having big tempers aren\'t  necessarily true, people should think twice before testing it with you. You choose whether you are size Medium or Small, but your speed is reduced by 5 feet either way.',
            '<b>Fat.</b> It\’s not big boned, you’ve accepted that. You are not slightly overweight. Your speed is reduced by 5 feet.',
            '<b>Frail Frame.</b> You do not handle pain very well. Each time you suffer damage, you lose 1 additional hit point.',
            '<b>Albino.</b> You suffer from a condition resulting in a complete lack of melanin. When in direct sunlight, you have disadvantage with Wisdom (Perception) checks when using your eyes.',
            '<b>Dyslexia.</b> You have disadvantage on checks that involve reading or research unless you take double the usual time to perform them.',
            '<b>Shyness.</b> You don\’t like being in public spaces. You have disadvantage with all Charisma ability checks.'
          ];

    var dRoll = rolldice(0, (sc1.length - 1));
    var dData = '';

    dData += sc1[dRoll];

    return dData;
}

// ////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Menu Buttons below /////////////////////////////////////////////////////////////////////////////////////////
// ////////////////////////////////////////////////////////////////////////////////////////////////////////////

function buttonGenerate(apex) {
    var isApex = apex == true ? true : false; 
    var dData = '<b>Parenting:</b><br />' + parenting(); 
    dData += '<b>Siblings:</b><br />' + siblings(); 
    dData += '<b>Life Events:</b><br /><br />'; 

    var Le = rolldice(5, 10);

    for (i = 0; i < Le; i++) {
        dData += lifeEpisodes(isApex); 
    }

    document.getElementById("origin").innerHTML = dData;
}

function buttonGeneticBenefit() {
    var dData = '<b>Genetic Benefit:</b><br />' + geneticBenefit(); 

    document.getElementById("origin").innerHTML = dData;
}

function buttonShortComings() {
    var dData = '<b>Shortcomings:</b><br />' + shortComings(); 

    document.getElementById("origin").innerHTML = dData;
}</script>
</div>


            </article>

        </section>
    </body>
</html>
