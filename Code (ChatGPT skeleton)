#include <JuceHeader.h>

class PhaseModulationPlugin : public juce::AudioProcessor
{
public:
    PhaseModulationPlugin()
    {
        // Set up the parameters for the plugin
        addParameter(phaseModulationAmount = new juce::AudioParameterFloat("phaseModulationAmount", "Phase Modulation Amount", 0.0f, 1.0f, 0.5f));
    }

    void prepareToPlay(double sampleRate, int samplesPerBlock) override
    {
        // Set up the audio processing objects
        phaseModulationBuffer.setSize(1, samplesPerBlock);
    }

    void releaseResources() override
    {
        // Release the audio processing objects
        phaseModulationBuffer.setSize(0, 0);
    }

    void processBlock(juce::AudioBuffer<float>& buffer, juce::MidiBuffer&) override
    {
        // Get the sidechain buffer
        const float* sidechainBuffer = sidechain.getReadPointer(0);

        // Get the audio buffer
        float* audioBuffer = buffer.getWritePointer(0);

        // Process each sample in the buffer
        for (int i = 0; i < buffer.getNumSamples(); ++i)
        {
            // Calculate the phase modulation amount
            float phaseModulation = *phaseModulationAmount * sidechainBuffer[i];

            // Calculate the phase modulation buffer
            phaseModulationBuffer.setSample(0, i, std::sin(phaseModulation));

            // Apply the phase modulation to the audio sample
            audioBuffer[i] *= phaseModulationBuffer.getSample(0, i);
        }
    }

    juce::AudioProcessorEditor* createEditor() override
    {
        // Create a default editor
        return new juce::GenericAudioProcessorEditor(*this);
    }

    bool hasEditor() const override
    {
        // The plugin has an editor
        return true;
    }

    const juce::String getName() const override
    {
        // Return the name of the plugin
        return "Phase Modulation Plugin";
    }

    bool acceptsMidi() const override
    {
        // The plugin does not accept MIDI input
        return false;
    }

    bool producesMidi() const override
    {
        // The plugin does not produce MIDI output
        return false;
    }

    double getTailLengthSeconds() const override
    {
        // The plugin has no tail
        return 0.0;
    }

    int getNumPrograms() override
    {
        // The plugin has one program
        return 1;
    }

    int getCurrentProgram() override
    {
        // The plugin is always on the first program
        return 0;
    }

    void setCurrentProgram(int index) override
    {
        // The plugin only has one program
    }

    const juce::String getProgramName(int index) override
    {
        // The plugin only has one program
        return "Default";
    }

    void changeProgramName(int index, const juce::String& newName) override
    {
        // The plugin only has one program
    }

    void getStateInformation(juce::MemoryBlock& destData) override
    {
        // The plugin has no state information
    }

    void setStateInformation(const void* data, int sizeInBytes) override
    {
        // The plugin has no state information
    }

private:
    juce::AudioParameterFloat* phaseModulationAmount;
    juce::AudioBuffer<float> phaseModulationBuffer{ 1, 1 };
    juce::AudioBuffer<float> sidechain{ 1, 1 };
};

juce::AudioProcessor* JUCE_CALLTYPE createPluginFilter()
{
    return new PhaseModulationPlugin();
}
