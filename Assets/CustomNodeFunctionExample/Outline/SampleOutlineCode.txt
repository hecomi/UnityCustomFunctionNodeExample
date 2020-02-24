#ifndef SAMPLE_OUTLINE_INCLUDED
#define SAMPLE_OUTLINE_INCLUDED

void SampleOutline_float(
    Texture2D Texture,
    float2 UV,
    SamplerState Sampler,
    float Outline,
    out float Alpha)
{
    Alpha = 0.0;
    float r = Outline;

    Alpha += SAMPLE_TEXTURE2D(Texture, Sampler, UV + float2(+r,  0)).a;
    Alpha += SAMPLE_TEXTURE2D(Texture, Sampler, UV + float2(-r,  0)).a;
    Alpha += SAMPLE_TEXTURE2D(Texture, Sampler, UV + float2( 0, +r)).a;
    Alpha += SAMPLE_TEXTURE2D(Texture, Sampler, UV + float2( 0, -r)).a;
    Alpha = min(Alpha, 1.0);

    Alpha -= SAMPLE_TEXTURE2D(Texture, Sampler, UV).a;
    Alpha = max(Alpha, 0.0);
}

#endif
