<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Drawabox Lesson 1 Critique Generator</title>
    <style>
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; line-height: 1.6; margin: 0; padding: 20px; background-color: #f8f9fa; color: #343a40; }
        .container { max-width: 800px; margin: 0 auto; background-color: #ffffff; padding: 30px; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.08); }
        h1, h2, h3 { color: #212529; border-bottom: 2px solid #e9ecef; padding-bottom: 10px; margin-top: 2em; }
        h1 { text-align: center; border-bottom: none; }
        .intro-principles { background-color: #e9ecef; padding: 20px; border-radius: 5px; margin-bottom: 30px; }
        .intro-principles ul { padding-left: 20px; margin: 0; }
        .critique-point, .general-feedback-point { margin-bottom: 15px; padding: 12px 15px; border-left: 3px solid #ced4da; border-radius: 4px; transition: border-color 0.3s, background-color 0.2s; }
        .critique-point { cursor: pointer; }
        .critique-point:hover { border-left-color: #007bff; background-color: #f1f3f5; }
        #general-feedback .general-feedback-point { border-left-color: #fd7e14; }
        #revisions-section .critique-point { border-left-color: #dc3545; }
        #revisions-section .critique-point:hover { border-left-color: #c82333; }
        label { display: flex; align-items: center; font-weight: bold; cursor: pointer; width: 100%; }
        input[type="checkbox"] { transform: scale(1.5); margin-right: 20px; margin-left: 5px; }
        .general-feedback-point .options-group { display: flex; gap: 15px; margin-top: 8px; flex-wrap: wrap; }
        .general-feedback-point .options-group label { font-weight: normal; cursor: pointer; }
        .general-feedback-point .options-group input[type="radio"] { transform: scale(1.2); margin-right: 5px; }
        .general-feedback-point > label { font-weight: bold; }
        #critique-generator { margin-top: 40px; padding: 20px; background-color: #f8f9fa; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); text-align: center; }
        #generated-critique { width: 100%; height: 300px; margin-top: 15px; padding: 15px; border: 1px solid #ced4da; border-radius: 5px; white-space: pre-wrap; box-sizing: border-box; background-color: #fff; }
        .button-group { margin-top: 20px; display: flex; justify-content: center; gap: 15px; }
        button { padding: 12px 25px; font-size: 16px; font-weight: bold; border: none; border-radius: 5px; cursor: pointer; transition: background-color 0.3s, transform 0.1s; }
        button:active { transform: translateY(1px); }
        #generate-btn { background-color: #007bff; color: white; }
        #generate-btn:hover { background-color: #0056b3; }
        #copy-btn, #reset-btn { background-color: #6c757d; color: white; }
        #copy-btn:hover, #reset-btn:hover { background-color: #5a6268; }
        .toast-message { position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); background-color: #28a745; color: white; padding: 10px 20px; border-radius: 5px; z-index: 1000; opacity: 0; transition: opacity 0.5s; }
        .revision-dropdown-container { margin-top: 15px; padding-left: 35px; }
        .revision-dropdown-container p { margin: 0 0 5px 0; font-size: 0.9em; font-weight: normal; color: #555; text-align: left; }
        .revision-select { width: 100%; min-height: 80px; border-radius: 4px; border: 1px solid #ced4da; padding: 5px; }
        .revision-select option { padding: 5px; font-size: 14px; }
    </style>
</head>
<body>

    <div class="container">
        <h1>Lesson 1 Critique Generator</h1>
        
        <div class="intro-principles"> ... </div>

        <div id="general-feedback">
            <h2>General Feedback</h2>
            <div class="general-feedback-point">
                <label>Tool Usage</label>
                <div class="options-group">
                    <label><input type="radio" name="tool-usage" value="ignore" checked> Ignore</label>
                    <label><input type="radio" name="tool-usage" value="fineliner_good"> Good (Fineliner)</label>
                    <label><input type="radio" name="tool-usage" value="ballpoint_okay"> Okay (Ballpoint)</label>
                    <label><input type="radio" name="tool-usage" value="other_bad"> Bad (Other)</label>
                </div>
            </div>
            <div class="general-feedback-point">
                <label>Overall Line Quality</label>
                <div class="options-group">
                    <label><input type="radio" name="line-quality" value="ignore" checked> Ignore</label>
                    <label><input type="radio" name="line-quality" value="good"> Good</label>
                    <label><input type="radio" name="line-quality" value="okay"> Okay</label>
                    <label><input type="radio" name="line-quality" value="bad"> Bad</label>
                </div>
            </div>
            <div class="general-feedback-point">
                <label>Line Execution Style</label>
                <div class="options-group">
                    <label><input type="radio" name="line-style" value="ignore" checked> Ignore</label>
                    <label><input type="radio" name="line-style" value="good"> Good (Drawing)</label>
                    <label><input type="radio" name="line-style" value="bad"> Bad (Scratchy)</label>
                </div>
            </div>
            <div class="general-feedback-point">
                <label>Following Instructions</label>
                <div class="options-group">
                    <label><input type="radio" name="instructions" value="ignore" checked> Ignore</label>
                    <label><input type="radio" name="instructions" value="good"> Good</label>
                    <label><input type="radio" name="instructions" value="bad"> Bad</label>
                </div>
            </div>
            <div class="general-feedback-point">
                <label>3D Thinking</label>
                <div class="options-group">
                    <label><input type="radio" name="thinking-3d" value="ignore" checked> Ignore</label>
                    <label><input type="radio" name="thinking-3d" value="good"> Good</label>
                    <label><input type="radio" name="thinking-3d" value="bad"> Bad</label>
                </div>
            </div>
             <div class="general-feedback-point">
                <label>Drawing Medium</label>
                <div class="options-group">
                    <label><input type="radio" name="medium" value="ignore" checked> Ignore</label>
                    <label><input type="radio" name="medium" value="digital"> Digital Tablet</label>
                </div>
            </div>
        </div>

        <div class="exercise-section" id="section-lines">
            <h2>Lines</h2>
            <h3>Superimposed Lines</h3>
            <div class="critique-point"><label><input type="checkbox" id="wobble-superimposed" data-context-group="wobble" data-exercise-name="Superimposed Lines">Lines are wobbly</label></div>
            <div class="critique-point"><label><input type="checkbox" id="arc-superimposed" data-context-group="arc" data-exercise-name="Superimposed Lines">Lines are arcing</label></div>
            <div class="critique-point"><label><input type="checkbox" id="fraying-superimposed">There is fraying</label></div>
            <h3>Ghosted Lines</h3>
            <div class="critique-point"><label><input type="checkbox" id="wobble-ghosted" data-context-group="wobble" data-exercise-name="Ghosted Lines">Lines are wobbly</label></div>
            <div class="critique-point"><label><input type="checkbox" id="arc-ghosted" data-context-group="arc" data-exercise-name="Ghosted Lines">Lines are arcing</label></div>
            <h3>Ghosted Planes</h3>
            <div class="critique-point"><label><input type="checkbox" id="planes-rushing">Line quality drops</label></div>
        </div>
        
        <div class="exercise-section" id="section-ellipses">
            <h2>Ellipses</h2>
            <h3>Tables of Ellipses</h3>
            <div class="critique-point"><label><input type="checkbox" id="drawthrough-tables" data-context-group="drawthrough" data-exercise-name="Tables of Ellipses">Not drawing through 2-3 times</label></div>
            <div class="critique-point"><label><input type="checkbox" id="overdraw-tables" data-context-group="overdraw" data-exercise-name="Tables of Ellipses">Drawing through too many times</label></div>
            <div class="critique-point"><label><input type="checkbox" id="snugly-tables" data-context-group="snugly" data-exercise-name="Tables of Ellipses">Not fitting snugly</label></div>
            <div class="critique-point"><label><input type="checkbox" id="shape-tables" data-context-group="shape" data-exercise-name="Tables of Ellipses">Unevenly shaped / wobbly</label></div>
            <h3>Ellipses in Planes</h3>
             <div class="critique-point"><label><input type="checkbox" id="drawthrough-planes" data-context-group="drawthrough" data-exercise-name="Ellipses in Planes">Not drawing through 2-3 times</label></div>
             <div class="critique-point"><label><input type="checkbox" id="overdraw-planes" data-context-group="overdraw" data-exercise-name="Ellipses in Planes">Drawing through too many times</label></div>
             <div class="critique-point"><label><input type="checkbox" id="snugly-planes" data-context-group="snugly" data-exercise-name="Ellipses in Planes">Not touching all 4 edges</label></div>
             <div class="critique-point"><label><input type="checkbox" id="shape-planes" data-context-group="shape" data-exercise-name="Ellipses in Planes">Unevenly shaped / wobbly</label></div>
            <h3>Funnels</h3>
             <div class="critique-point"><label><input type="checkbox" id="drawthrough-funnels" data-context-group="drawthrough" data-exercise-name="Funnels">Not drawing through 2-3 times</label></div>
             <div class="critique-point"><label><input type="checkbox" id="overdraw-funnels" data-context-group="overdraw" data-exercise-name="Funnels">Drawing through too many times</label></div>
             <div class="critique-point"><label><input type="checkbox" id="snugly-funnels" data-context-group="snugly" data-exercise-name="Funnels">Not touching the sides</label></div>
             <div class="critique-point"><label><input type="checkbox" id="shape-funnels" data-context-group="shape" data-exercise-name="Funnels">Unevenly shaped / wobbly</label></div>
             <div class="critique-point"><label><input type="checkbox" id="aligned-funnels">Not aligned to the minor axis</label></div>
        </div>

        <div class="exercise-section" id="section-boxes">
            <h2>Boxes</h2>
            <h3>Plotted Perspective</h3>
            <div class="critique-point"><label><input type="checkbox" id="plotted-ruler">Not using a ruler</label></div>
            <div class="critique-point"><label><input type="checkbox" id="plotted-verticals">Verticals not perpendicular</label></div>
            <div class="critique-point"><label><input type="checkbox" id="plotted-vps">Horizontals not plotted to VPs</label></div>
            <h3>Rough Perspective</h3>
            <div class="critique-point"><label><input type="checkbox" id="wobble-rough" data-context-group="wobble" data-exercise-name="Rough Perspective">Lines are wobbly</label></div>
            <div class="critique-point"><label><input type="checkbox" id="arc-rough" data-context-group="arc" data-exercise-name="Rough Perspective">Lines are arcing</label></div>
            <div class="critique-point"><label><input type="checkbox" id="rough-1vp">Not using 1 vanishing point</label></div>
            <div class="critique-point"><label><input type="checkbox" id="rough-rectangular">Faces not rectangular</label></div>
            <div class="critique-point"><label><input type="checkbox" id="rough-extensions">Not using line extensions</label></div>
            <div class="critique-point"><label><input type="checkbox" id="rough-xray">Not drawing through boxes</label></div>
            <h3>Rotated Boxes</h3>
            <div class="critique-point"><label><input type="checkbox" id="wobble-rotated" data-context-group="wobble" data-exercise-name="Rotated Boxes">Lines are wobbly</label></div>
            <div class="critique-point"><label><input type="checkbox" id="arc-rotated" data-context-group="arc" data-exercise-name="Rotated Boxes">Lines are arcing</label></div>
            <div class="critique-point"><label><input type="checkbox" id="rotated-core">Core steps not followed</label></div>
            <div class="critique-point"><label><input type="checkbox" id="rotated-gaps">Gaps are loose/inconsistent</label></div>
            <div class="critique-point"><label><input type="checkbox" id="rotated-not-rotating">Boxes are not actually rotating</label></div>
            <div class="critique-point"><label><input type="checkbox" id="rotated-xray">Not drawing through boxes</label></div>
            <div class="critique-point"><label><input type="checkbox" id="rotated-all-boxes">Not all boxes drawn</label></div>
            <h3>Organic Perspective</h3>
            <div class="critique-point"><label><input type="checkbox" id="wobble-organic" data-context-group="wobble" data-exercise-name="Organic Perspective">Lines are wobbly</label></div>
            <div class="critique-point"><label><input type="checkbox" id="arc-organic" data-context-group="arc" data-exercise-name="Organic Perspective">Lines are arcing</label></div>
            <div class="critique-point"><label><input type="checkbox" id="organic-divergence">Edges are diverging</label></div>
            <div class="critique-point"><label><input type="checkbox" id="organic-foreshortening">Dramatic foreshortening</label></div>
            <div class="critique-point"><label><input type="checkbox" id="organic-variety">Boxes lack variety / appear 'flat'</label></div>
        </div>

        <div id="revisions-section">
            <h2>Next Steps & Revisions</h2>
            <div class="critique-point">
                <label><input type="checkbox" id="assign-revision-lines"> Assign Revisions for Lines</label>
                <div class="revision-dropdown-container" style="display: none;">
                    <p>Select the main reason(s) for revision (Ctrl/Cmd + Click for multiple):</p>
                    <select multiple id="revision-select-lines" class="revision-select"></select>
                </div>
            </div>
            <div class="critique-point">
                <label><input type="checkbox" id="assign-revision-ellipses"> Assign Revisions for Ellipses</label>
                <div class="revision-dropdown-container" style="display: none;">
                    <p>Select the main reason(s) for revision (Ctrl/Cmd + Click for multiple):</p>
                    <select multiple id="revision-select-ellipses" class="revision-select"></select>
                </div>
            </div>
            <div class="critique-point">
                <label><input type="checkbox" id="assign-revision-boxes"> Assign Revisions for Boxes</label>
                <div class="revision-dropdown-container" style="display: none;">
                    <p>Select the main reason(s) for revision (Ctrl/Cmd + Click for multiple):</p>
                    <select multiple id="revision-select-boxes" class="revision-select"></select>
                </div>
            </div>
        </div>
        
        <div id="critique-generator">
            <h2>Your Generated Critique</h2>
            <p>Click the button below to compile the feedback based on your selections.</p>
            <button id="generate-btn">Generate Critique</button>
            <textarea id="generated-critique" placeholder="Your personalized critique will appear here..."></textarea>
            <div class="button-group">
                <button id="copy-btn">Copy to Clipboard</button>
                <button id="reset-btn">Reset</button>
            </div>
        </div>
    </div>
    
    <div id="toast" class="toast-message">Copied to clipboard!</div>

    <script>
        let critiqueData = {}; 

        document.addEventListener('DOMContentLoaded', () => {
            loadCritiqueData();
            document.getElementById('generate-btn').addEventListener('click', generateCritique);
            document.getElementById('copy-btn').addEventListener('click', copyCritique);
            document.getElementById('reset-btn').addEventListener('click', resetForm);

            document.querySelectorAll('.critique-point').forEach(row => {
                const checkbox = row.querySelector('input[type="checkbox"]');
                if (checkbox) {
                    const label = row.querySelector('label');
                    const isRevisionCheckbox = checkbox.id.startsWith('assign-revision');

                    const clickHandler = (event) => {
                        if (event.target.tagName === 'SELECT' || event.target.tagName === 'OPTION') return;
                        if (event.target === row || event.target === label || event.target.parentElement === label) {
                             if(event.target !== checkbox) checkbox.checked = !checkbox.checked;
                            if (isRevisionCheckbox) {
                                checkbox.dispatchEvent(new Event('change'));
                            }
                        }
                    };
                    
                    row.addEventListener('click', clickHandler);

                    if(isRevisionCheckbox){
                        checkbox.addEventListener('change', () => toggleRevisionDropdown(checkbox.id.split('-')[2]));
                    }
                }
            });
        });
        
        function toggleRevisionDropdown(sectionKey) {
            const checkbox = document.getElementById(`assign-revision-${sectionKey}`);
            const container = checkbox.closest('.critique-point').querySelector('.revision-dropdown-container');
            const select = document.getElementById(`revision-select-${sectionKey}`);
            
            if (checkbox.checked) {
                select.innerHTML = '';
                const mistakeCheckboxes = document.querySelectorAll(`#section-${sectionKey} input[type="checkbox"]:checked`);
                
                if (mistakeCheckboxes.length > 0) {
                    mistakeCheckboxes.forEach(cb => {
                        const option = document.createElement('option');
                        option.value = cb.id;
                        option.textContent = critiqueData[cb.id]?.reason || cb.parentElement.textContent.trim();
                        select.appendChild(option);
                    });
                    container.style.display = 'block';
                } else {
                    const option = document.createElement('option');
                    option.textContent = "No mistakes selected in this section.";
                    option.disabled = true;
                    select.appendChild(option);
                    container.style.display = 'block';
                }
            } else {
                container.style.display = 'none';
            }
        }

        // --- NEW, REWRITTEN, AND FUNCTIONAL GENERATE CRITIQUE ---
        function generateCritique() {
            let critiqueText = "Hello! Here is your feedback for the Lesson 1 exercises. Overall, great work completing the homework.\n\n";
            let pointCounter = 1;
            const pointNumberMap = {};
            const processedContextGroups = new Set();
            
            // GENERAL FEEDBACK
            let generalFeedback = "";
            const generalSelectors = {
                'tool-usage': 'general-tools', 'line-quality': 'general-wobbly', 'line-style': 'general-scratchy',
                'instructions': 'general-instructions', 'thinking-3d': 'general-3d', 'medium': 'general-digital'
            };
            for (const name in generalSelectors) {
                const selectedValue = document.querySelector(`input[name="${name}"]:checked`)?.value;
                const dataKey = generalSelectors[name];
                const feedbackData = critiqueData[dataKey];
                if (selectedValue && selectedValue !== 'ignore' && feedbackData && feedbackData[selectedValue]) {
                     generalFeedback += `*   ${feedbackData[selectedValue]}\n\n`;
                }
            }
            if (generalFeedback) {
                critiqueText += `**Overall Feedback**\n${generalFeedback}---\n\n`;
            }
            
            critiqueText += "Here is the feedback broken down by exercise:\n\n";

            // CONTEXT-AWARE & REGULAR FEEDBACK COMBINED
            const sections = { 'Lines': 'lines', 'Ellipses': 'ellipses', 'Boxes': 'boxes' };
            for (const sectionTitle in sections) {
                let sectionContent = "";
                const container = document.getElementById(`section-${sectionTitle.toLowerCase()}`);
                const subheadings = container.getElementsByTagName('h3');
                
                for (let h3 of subheadings) {
                    let subSectionContent = "";
                    let nextElem = h3.nextElementSibling;
                    while (nextElem && nextElem.classList.contains('critique-point')) {
                        const checkbox = nextElem.querySelector('input[type="checkbox"]');
                        if (checkbox) {
                            const data = critiqueData[checkbox.id];
                            if (checkbox.checked) {
                                subSectionContent += `${pointCounter}. ${data.critique}\n\n`;
                                pointNumberMap[checkbox.id] = pointCounter;
                                pointCounter++;
                            } else {
                                subSectionContent += `+ ${data.praise}\n\n`;
                            }
                        }
                        nextElem = nextElem.nextElementSibling;
                    }
                    if (subSectionContent) {
                        sectionContent += `**${h3.textContent}**\n${subSectionContent}`;
                    }
                }
                if (sectionContent) {
                    critiqueText += `### ${sectionTitle}\n${sectionContent}`;
                }
            }
            
            // REVISIONS
            let assignedRevisions = [];
            ['lines', 'ellipses', 'boxes'].forEach(key => {
                 if (document.getElementById(`assign-revision-${key}`).checked) {
                    const select = document.getElementById(`revision-select-${key}`);
                    const selectedOptions = Array.from(select.selectedOptions);
                    let reasons = [];
                    selectedOptions.forEach(option => {
                        const cbId = option.value;
                        if (pointNumberMap[cbId]) {
                            reasons.push({ text: critiqueData[cbId].reason, number: pointNumberMap[cbId] });
                        }
                    });
                     if (reasons.length > 0) {
                        assignedRevisions.push({ name: key.charAt(0).toUpperCase() + key.slice(1), reasons: reasons });
                    }
                 }
            });

            critiqueText += "\n---\n\n### Next Steps\n";
            if (assignedRevisions.length > 0) {
                critiqueText += "Based on the feedback above, I've assigned the following revision(s). Please focus on the points mentioned and resubmit your work for review.\n\n**Assigned Revision(s):**\n";
                assignedRevisions.forEach(rev => {
                    critiqueText += `*   **${rev.name}:**\n`;
                    rev.reasons.forEach(reason => {
                        critiqueText += `    *   [${reason.text}](${reason.number})\n`;
                    });
                });
            } else {
                critiqueText += "Excellent work on this lesson! Your grasp of the material is strong enough to move forward. You can now proceed to the **250 Box Challenge**. Remember to incorporate all of these Lesson 1 exercises into your regular warmups.";
            }

            critiqueText += "\n\nKeep up the great work, and let me know if you have any questions!";
            document.getElementById('generated-critique').value = critiqueText;
        }

        function copyCritique() {
            const critiqueArea = document.getElementById('generated-critique');
            if (critiqueArea.value) {
                critiqueArea.select();
                navigator.clipboard.writeText(critiqueArea.value).then(() => {
                    const toast = document.getElementById('toast');
                    toast.style.opacity = 1;
                    setTimeout(() => { toast.style.opacity = 0; }, 2000);
                });
            }
        }

        function resetForm() {
            document.querySelectorAll('input[type="checkbox"]').forEach(checkbox => checkbox.checked = false);
             document.querySelectorAll('input[type="radio"]').forEach(radio => {
                if (radio.value === 'ignore') radio.checked = true;
            });
            document.getElementById('generated-critique').value = '';
            document.querySelectorAll('.revision-dropdown-container').forEach(container => container.style.display = 'none');
        }
        
        function loadCritiqueData() {
             critiqueData = { /* All data from previous version */ };
             const fullData = {
                "general-tools": { fineliner_good: "Thank you for using the recommended tools (fineliners). This gives your lines a crisp, clear quality.", ballpoint_okay: "Good job on using a ballpoint pen. It's a perfectly acceptable alternative to fineliners for these exercises, including the 250 Box Challenge. It is still highly recommended to switch to fineliners when you can, as they will make assessing your own linework much easier.", other_bad: "It appears you might not be using a fineliner or ballpoint pen. Using a pencil, for example, can hide issues in your linework. Please switch to a recommended tool." },
                "general-wobbly": { good: "Your overall line quality is excellent. Your marks are confident, smooth, and consistent.", bad: "A general theme is that your lines are often wobbly. This usually points to hesitation and drawing from the wrist/elbow. Focus on using the ghosting method and drawing from your shoulder.", okay: "Your line quality is generally solid. There are some minor wobbles, but for the most part, you're drawing with confidence. Keep focusing on that smooth, single stroke." },
                "general-scratchy": { good: "Your line execution is great. You're consistently 'drawing' your lines in single, fluid strokes rather than 'sketching' them.", bad: "There's a tendency to 'sketch' or 'chisel' your lines using multiple, short, overlapping strokes. For these exercises, it's crucial to focus on drawing each line as a single, confident mark after ghosting." },
                "general-instructions": { good: "Your work shows an excellent level of care and attention to detail. You've clearly read and followed the instructions for each exercise thoroughly.", bad: "One thing to focus on is your attention to the instructions. I noticed in a few places that some key steps or rules might have been missed. Drawabox is very process-oriented, so following each step is crucial." },
                "general-3d": { good: "You're doing a fantastic job of thinking and drawing in three dimensions. Your boxes feel solid and volumetric.", bad: "A key goal for this lesson is to shift from drawing flat shapes to constructing solid 3D forms. Focus on visualizing each box as a real object in space. Consistently 'drawing through' every box is the best way to strengthen this." },
                "general-digital": { digital: "As a digital artist, be extra mindful of the course's core principles. Avoid relying on stabilizers or the undo function, as they can hinder the development of raw confidence and muscle memory. Treat each stroke as if it were permanent, just like with traditional ink." },
                'wobble-superimposed': { praise: 'Lines are confident and straight.', critique: 'In Superimposed Lines, your lines wobble, suggesting a fear of inaccuracy. Focus only on the end point and commit to a smooth, single stroke.', reason: 'Lines wobble' },
                'arc-superimposed': { praise: 'Lines are straight.', critique: 'In Superimposed Lines, your lines are arcing. This is a sign of drawing from the wrist/elbow instead of the shoulder.', reason: 'Lines are arcing' },
                'fraying-superimposed': { praise: 'Line starts are clean.', critique: 'There is fraying at the start of your lines, which suggests rushing. Place your pen down deliberately before starting the stroke.', reason: 'Fraying lines' },
                'wobble-ghosted': { praise: 'Lines are confident and straight.', critique: 'In Ghosted Lines, your lines wobble, suggesting hesitation during the execution phase. Remember to commit to the stroke once your pen touches the page.', reason: 'Lines wobble' },
                'arc-ghosted': { praise: 'Lines are straight.', critique: 'In Ghosted Lines, your lines are arcing. Make sure you are engaging your shoulder to compensate for the natural arc of your arm.', reason: 'Lines are arcing' },
                'planes-rushing': { praise: 'Line quality is consistent.', critique: 'Line quality drops in the Ghosted Planes exercise. This suggests you may be rushing due to the quantity of work. Give each line the same focus and attention.', reason: 'Line quality drops' },
                'drawthrough-tables': { praise: 'Ellipses are drawn through correctly.', critique: 'In Tables of Ellipses, you are not drawing through your ellipses two full times. This is a critical step for building muscle memory.', reason: 'Not drawing through 2-3 times' },
                'overdraw-tables': { praise: 'Ellipses have the correct number of rotations.', critique: 'You are drawing through your ellipses far more than the recommended 2-3 times. This can become a crutch. Limit yourself to just two confident rotations.', reason: 'Drawing through too many times' },
                'snugly-tables': { praise: 'Ellipses fit well in their spaces.', critique: 'In Tables of Ellipses, your ellipses are not fitting snugly against the borders. Remember that this is the goal of the exercise.', reason: 'Not fitting snugly' },
                'shape-tables': { praise: 'Ellipses are smooth and evenly shaped.', critique: 'In Tables of Ellipses, your ellipses are uneven or wobbly. This suggests hesitation or drawing from the wrist. Use your shoulder and the ghosting method.', reason: 'Ellipses are uneven' },
                'drawthrough-planes': { praise: 'Ellipses are drawn through correctly.', critique: 'In Ellipses in Planes, you are not drawing through your ellipses two full times.', reason: 'Not drawing through 2-3 times' },
                'overdraw-planes': { praise: 'Ellipses have the correct number of rotations.', critique: 'In Ellipses in Planes, you are drawing through your ellipses too many times.', reason: 'Drawing through too many times' },
                'snugly-planes': { praise: 'Ellipses fit well in their spaces.', critique: 'In Ellipses in Planes, your ellipses are not touching all 4 edges of the plane. Remember to aim for the borders.', reason: 'Not touching all 4 edges' },
                'shape-planes': { praise: 'Ellipses are smooth and evenly shaped.', critique: 'In Ellipses in Planes, your ellipses are uneven or deformed. Prioritize a confident execution even if it makes fitting them harder at first.', reason: 'Ellipses are uneven' },
                'drawthrough-funnels': { praise: 'Ellipses are drawn through correctly.', critique: 'In Funnels, you are not drawing through your ellipses two full times.', reason: 'Not drawing through 2-3 times' },
                'overdraw-funnels': { praise: 'Ellipses have the correct number of rotations.', critique: 'In Funnels, you are drawing through your ellipses too many times.', reason: 'Drawing through too many times' },
                'snugly-funnels': { praise: 'Ellipses fit well in their spaces.', critique: 'In Funnels, your ellipses are not touching the sides of the funnel.', reason: 'Not touching the sides' },
                'shape-funnels': { praise: 'Ellipses are smooth and evenly shaped.', critique: 'In Funnels, your ellipses are uneven or wobbly.', reason: 'Ellipses are uneven' },
                'aligned-funnels': { praise: 'Ellipses are well-aligned.', critique: 'In Funnels, your ellipses are not consistently aligned to the central minor axis. Show that you are attempting this, even if it is not perfect.', reason: 'Not aligned to minor axis' },
                'plotted-ruler': { praise: 'Used a ruler correctly.', critique: 'The Plotted Perspective exercise requires a ruler. It appears you have drawn your lines freehand.', reason: 'Not using a ruler' },
                'plotted-verticals': { praise: 'Verticals are straight.', critique: 'Your vertical lines in Plotted Perspective are not perpendicular to the horizon. Take more time to align your ruler.', reason: 'Verticals not perpendicular' },
                'plotted-vps': { praise: 'Horizontals are plotted correctly.', critique: 'Your horizontal lines in Plotted Perspective are not all aimed correctly at the vanishing points.', reason: 'Horizontals not aimed at VPs' },
                'wobble-rough': { praise: 'Lines are confident.', critique: 'In Rough Perspective, your lines are wobbly.', reason: 'Lines are wobbly' },
                'arc-rough': { praise: 'Lines are straight.', critique: 'In Rough Perspective, your lines are arcing.', reason: 'Lines are arcing' },
                'rough-1vp': { praise: 'Using 1 VP correctly.', critique: 'Rough Perspective must be done in 1-point perspective. It looks like you may be using two.', reason: 'Not using 1 VP' },
                'rough-rectangular': { praise: 'Faces are rectangular.', critique: 'The front and back faces of your boxes in Rough Perspective must be rectangular. Some of yours are tilted.', reason: 'Faces not rectangular' },
                'rough-extensions': { praise: 'Line extensions are used well.', critique: 'You are not using line extensions in Rough Perspective to check your accuracy. This is a critical step.', reason: 'Not using line extensions' },
                'rough-xray': { praise: 'Drawing through boxes.', critique: 'Remember to draw through your boxes in Rough Perspective. This is essential for understanding their 3D form.', reason: 'Not drawing through boxes' },
                'wobble-rotated': { praise: 'Lines are confident.', critique: 'In Rotated Boxes, your lines are wobbly.', reason: 'Lines are wobbly' },
                'arc-rotated': { praise: 'Lines are straight.', critique: 'In Rotated Boxes, your lines are arcing.', reason: 'Lines are arcing' },
                'rotated-core': { praise: 'Core steps followed.', critique: 'You missed the initial setup steps (axes and squares) for the Rotated Boxes exercise.', reason: 'Core steps missed' },
                'rotated-gaps': { praise: 'Gaps are tight.', critique: 'The gaps between your rotated boxes are too loose. Keep them packed tightly together.', reason: 'Makes estimation simpler.' },
                'rotated-not-rotating': { praise: 'Boxes are rotating correctly.', critique: 'Your boxes in Rotated Boxes do not appear to be truly rotating; their edges still converge to the same two vanishing points.', reason: 'Boxes are not rotating' },
                'rotated-xray': { praise: 'Drawing through boxes.', critique: 'Remember to draw through your rotated boxes with \'x-ray\' vision.', reason: 'Not drawing through boxes' },
                'rotated-all-boxes': { praise: 'Drew all boxes.', critique: 'You have missed some of the boxes in the Rotated Boxes set. Please complete the full set.', reason: 'Not all boxes drawn' },
                'wobble-organic': { praise: 'Lines are confident.', critique: 'In Organic Perspective, your lines are wobbly.', reason: 'Lines are wobbly' },
                'arc-organic': { praise: 'Lines are straight.', critique: 'In Organic Perspective, your lines are arcing.', reason: 'Lines are arcing' },
                'organic-divergence': { praise: 'No divergence.', critique: 'There are cases of divergence in your Organic Perspective boxes (parallel lines spreading apart).', reason: 'Lines are diverging' },
                'organic-foreshortening': { praise: 'Foreshortening is subtle.', critique: 'You are using very dramatic foreshortening in Organic Perspective. Try to keep it more gradual and subtle.', reason: 'Foreshortening too dramatic' },
                'organic-variety': { praise: 'Great variety in forms!', critique: 'Your boxes in Organic Perspective are very similar. Challenge yourself to create more variety by changing the initial \'Y\' angles and the proportions of the boxes.', reason: 'Boxes lack variety' }
            };

            for (const id in fullData) {
                critiqueData[id] = fullData[id];
                const contextGroup = document.getElementById(id)?.dataset.contextGroup;
                if (contextGroup && contextTemplates[contextGroup]) {
                    critiqueData[id].context = contextTemplates[contextGroup];
                }
            }
        }
    </script>
</body>
</html>
